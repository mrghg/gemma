#  GEOS-Chem-EnKF inverse model specification

This document is to describe features of the GEOS-Chem-EnKF inverse modelling system, which is common to all gases. 
Species-specific features or modifications are noted in the accompanying file for each species.

## Transport model

Brief overview of transport model, including appropriate references and version number(s).

We use GEOS-Chem version 14.3.1 - an Eulerian atmospheric chemistry and transport model which has been developed and managed by the GEOS-Chem Support Team, based at Harvard University (https://geoschem.github.io/index.html). 

### Scope

- Domain: 34.0°N -> 66.0°N; 15.0°W -> 35.0°E, 0.25°x0.3125° hor. resolution, 47 vertical levels
                                              0.5°x0.625° - hor. resolution of the inversion grid.
- Period: 2018-01-01 to 2019-12-31 (forward runs, 2018 - spinup, 2019 - analysis)
	  Jan, Jul 2019 (perturbed runs) - analysis, Dec, 2018 & Jun 2019 - needed for the inversion calculations (sequential). 

### Meteorology

- Which meteorological fields are used?
  The model is driven by GEOS FP meteorological re-analyses fields from the NASA Global Modelling and Assimilation Office (GMAO) Global Circulation Model.
- What horizontal, vertical and temporal resolution(s) is used (include any interpolation of the met. fields, and any difference between model transport and output resolutions)?
  0.25°x0.3125° hor. res., 47 vertical levels (surface -> 80.581 km (0.01 hPa), 3-h temporal res.

### Model input parameters

Note any specific model setup or parameters that are user/group specific (e.g., number of particles, etc.).

The model is run with atmospheric transport tilmestep = 300 s and emissions are converted to kg/m2/s using temporal profiles (monthly, day of week, hourly for anthropogenic sources) and chemical time step = 600 s.
Emissions are injected at the lowest model level, which is approximately 60 meters above ground level.  
 
## Inversion approach

Describe the inversion approach. If described in publication(s), provide appropriate references. If not described elsewhere, provide full details here.

We employ an Ensemble Kalman Filter (EnKF) system, specifically a variant known as the Local Ensemble Transform Kalman Filter (LETKF) (Hunt et al., 2007, Liu et al. (2016)).
The LETKF has been widely utilized in previous atmospheric inversion studies to infer emissions of the main green house gases - CO2 (e.g., Feng et al., 2009, Scarpelli et al., 2024) and CH4 (e.g., Lunt et. al, 2021) using the GEOS-Chem model as well as satellite/in-situ observations.
We employ a 15-day assimilation window and a one-month lag window, taking into account the influence of past emissions on our assimilation period.
We conduct our inversion sequentially, utilizing the posterior scale factors from a specific assimilation window to update the prior scale factors for the subsequent lag window, covering the same date range.
The inversion calculations are localized, meaning that the state vector is influenced by observations within a prescribed radius of influence (localization distance) ranging from 250 to 1000 km. 
The choice of localization distance depends on the application and the density of the observational network.

### Model and measurement uncertainties

Use this section to describe uncertainties relating to the measurements and model, which apply to all species. 

- What measurement averaging time is used (if any)?

  1-hour for monthly runs (Jan vs July)
  3-hour for long term runs (yearly)

- Are a subset of observations removed prior to the inversion. If so, what criteria are used (e.g., to remove measurements under stable conditions)?

  We keep only day-time observations (10-17 UTC). 
  We also keep only well-mixed atmosphere when the standard deviation of concentrations  is less than a species-specific threshold.

- How are measurement uncertainties used?

  Temporal standard deviation provide by the observational dataset.

- How are model uncertainties estimated?
    
  The model uncertainty, including atmospheric transport error, is prescribed and specific to each species.

- How are these different source of uncertainty combined?

  The model-measurement uncertainty is defined as added in quadrature of the measurement and model uncertainties  

- How is the model compared to the observations? Sampled at same time/location? Comparison of monthly means? Spatially averaged? Are uncertainty covariances used? Etc.

  The model is sampled at the nearest time and location of each observation, including the inlet height re in situ data. 

### Fluxes and uncertainties

- Over what time period are fluxes estimated (e.g., weekly, monthly). Note that this can be a scaling of a more finely time-resolved flux field.

  The fluxes are estimated for each assimilation window, which corresponds to a 15-day period

- Describe any spatial basis function decomposition that is used. How are basis functions calculated?
  
  Currenlty, we do not employ spatial basis function decomposition. 
  Our methodology involves conducting inversion calculations directly over the entire latitude-longitude grid. 
  Each grid cell is treated as an individual entity, and the state variables are updated based on observations and model forecasts without transforming them into basis functions. 

- What a priori uncertainty is assigned to each basis function? What prior PDF is used?
  
 Without the use of spatial basis function decomposition, a priori uncertainties are assigned directly to the flux estimates at each grid point of the inversion grid. This process involves constructing a covariance matrix P based on the geographical distances between grid points, followed by Cholesky decomposition. Random deviations within the specified standard deviation (0.5, 50%) are then sampled to generate ensemble perturbations (N = 100 ensemble members), enhancing the robustness of the inversion process. We assume an error correlation length for apriori uncertainty = 100 km. 

### Boundary conditions

- How are boundary conditions or baselines prescribed or estimated?
  
  We use three different datasets as boundary conditions and test their performance and effect on the posterio flux estimates. 
  The first product is obtained from a global run of the GEOS-Chem model (2° x 2.5° resolution) assimilated with usage of the satellite and flask observations.
  The second dataset is taken from the CAMS Greenhouse Gas inversion (https://www.copernicus.eu/en/access-data/copernicus-services-catalogue/cams-global-greenhouse-gas-inversion#:~:text=This%20data%20set%20contains%20net,and%20nitrous%20oxide%20(N20)). The data are global with specie-specific horizontal (1.9° x 3.75°, 2° x 3°)  and temporal (3-6 hours) resolutions.
  The third BCs dataset comes from the CAMS EGG4 satellite inversion (Agustí-Panareda et al., 2023) with 0.75° x 0.75° horizontal and 3 hour temporal resolutions.
  
- If estimated, what uncertainty is assigned to boundary conditions?

 In our inversion system, we incorporate uncertainties into the boundary conditions by perturbing them using a normal distribution (mean = 1.0, std = 0.05 (5%) ). We then solve for the perturbed boundary conditions during the inversion process. 


## References

Agustí-Panareda, A., Barré, J., Massart, S., Inness, A., Aben, I., Ades, M., Baier, B. C., Balsamo, G., Borsdorff, T., Bousserez, N., Boussetta, S., Buchwitz, M., Cantarello, L., Crevoisier, C., Engelen, R., Eskes, H., Flemming, J., Garrigues, S., Hasekamp, O., Huijnen, V., Jones, L., Kipling, Z., Langerock, B., McNorton, J., Meilhac, N., Noël, S., Parrington, M., Peuch, V.-H., Ramonet, M., Razinger, M., Reuter, M., Ribas, R., Suttie, M., Sweeney, C., Tarniewicz, J., and Wu, L.: Technical note: The CAMS greenhouse gas reanalysis from 2003 to 2020, Atmos. Chem. Phys., 23, 3829–3859, https://doi.org/10.5194/acp-23-3829-2023, 2023.

Feng, L., Palmer, P. I., Bösch, H., and Dance, S.: Estimating surface CO2 fluxes from space-borne CO2 dry air mole fraction observations using an ensemble Kalman Filter, Atmos. Chem. Phys., 9, 2619–2633, https://doi.org/10.5194/acp-9-2619-2009, 2009.

Hunt, B. R., Kostelich, E. J., & Szunyogh, I. (2007). Efficient data assimilation for spatiotemporal chaos: A local ensemble transform Kalman filter. Physica D: Nonlinear Phenomena, 230(1-2), 112-126

Liu, Y., Xiao, H., & Sun, W. (2016). Ensemble Kalman filter for parameter estimation in a land surface model. Advances in Meteorology, 2016, 1-11.

Lunt, M. F., Ganesan, A. L., Rigby, M., Marshall, J., O'Doherty, S., Myhre, C. L., ... & Manning, A. J. (2021). Rain-fed pulses of methane from East Africa during 2018–2019 contributed to atmospheric growth rate. Environmental Research Letters, 16(2), 024021.

Scarpelli, T., Palmer, P., Lunt, M., Super, I., and Droste, A.: Verifying national inventory-based combustion emissions of CO2 across the UK and mainland Europe using satellite observations of atmospheric CO and CO2, EGUsphere [preprint], https://doi.org/10.5194/egusphere-2024-416, 2024.

