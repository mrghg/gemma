# GEOS-Chem-EnKF specification for CH4

Use this file to provide any species-specific inversion specifications, or modifications to the general approach outined in the overview.

## Fluxes

List of flux datasets, including any modifications:

- {TNO GHGco v5.0 emission inventory}
  - Reference: Super et al., 2020: https://doi.org/10.5194/acp-20-1795-2020 
               Kuenen et al., 2022: https://doi.org/10.5194/essd14-491-2022
  - Native spatial resolution: 0.1° x 0.05°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: yearly
    - Resampled to: hourly fluxes using monthly, hourly, and daily temporal profiles (done inside the GEOS-Chem model) 
                    converted to kg/m2/s using the model time step  

- {GFED4 biomass burning}
- Reference: Randerson et al., 2018: Global Fire Emissions Database, Version 4, (GFEDv4). ORNL DAAC, Oak Ridge, Tennessee, USA. https://doi.org/10.3334/ORNLDAAC/1293
  - Native spatial resolution: 0.25° x 0.25°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: daily 
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

- {Wetland emissions - JPL WetCHARTs v1.0}
- Reference: Bloom et al., 2019: https://doi.org/10.3334/ORNLDAAC/1502
  - Native spatial resolution: 0.5° x 0.5°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: monthly 
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

- {Geological Seeps}
- Reference: Etiope et. al., 2019: https://doi.org/10.5194/essd-11-1-2019
  - Native spatial resolution: 1.0° x 1.0°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: yearly
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

- {Termite emissions - CAMS-GLOB-TERM.v1.1}
- Reference: Doubalova, 2018: https://atmosphere.copernicus.eu/sites/default/files/2019-11/26_CAMS81_2017SC1_D81.3.4.1-201808_v1_APPROVED_Ver1.pdf
  - Native spatial resolution: 0.5° x 0.5°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: monthly
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

- {Soil absorption from MeMo model (Not perturbed!)}
- Reference: Murguia-Flores et al. 2018, GMD, https://doi.org/10.5194/gmd-11-2009-2018
  - Native spatial resolution: 1.0° x 1.0°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: monthly 
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

## Observations

Provide an obspack reference, if used. Otherwise, state which measurements have been used.

 ICOS (~ 50 sites availble for the model domain, PAL is not within the modelling domain):
- Obspack reference:
obspack_ch4_1_GLOBALVIEWplus_v6.0_2023-12-01
Multi-laboratory compilation of atmospheric methane data for the period 1983-2022; obspack_ch4_1_GLOBALVIEWplus_v6.0_2023-12-01; NOAA Earth System Research Laboratory, Global Monitoring Laboratory. http://doi.org/10.25925/20231001

- DECC:
  - Reference:
  - Sites: 'BSD','HFD','RGL','TAC',;
  - Inlet heights : '248magl','100magl','90magl','185magl';

Describe any modification to the observations, including:
- Removal of a subset of observations, if not described in the overview (describe criteria)
- Averaging/resampling

We keep only well-mixed atmosphere when the standard deviation of concentrations within the lowest 5 vertical levels (top ~ 600 m) in the model is < 25 ppb.
See the rest details in [the overview](./overview.md)

### Measurement/model uncertainty (optional)

Describe measurement/model uncertainty, if different to the overview.

The model uncertainty, including atmospheric transport error, is currently set to 15 ppb.
See the rest details in [the overview](./overview.md)  