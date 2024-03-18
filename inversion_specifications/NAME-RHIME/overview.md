# RHIME inverse model specification

This document is to describe features of the inverse modelling system, which is common to all gases. Species-specific features or modifications should be noted in the accompanying file for each species.

## Transport model

NAME model (version 7.2) developped by the UK Met Office (Muller et al. 2013) : it is a Langrangian particle model that we run backward in time. 

### Scope

- Domain (lon, lat range, or "global"): covering from 10.73N to 79.06N and from 97.9W to 39.38E (??? Took the Europe domain).
- Period: ???

### Meteorology

- Which meteorological fields are used? 
Meteorological fields from the UK Met Office Unified Model.
- What horizontal, vertical and temporal resolution(s) is used (include any interpolation of the met. fields, and any difference between model transport and output resolutions)?
???

### Model input parameters

Note any specific model setup or parameters that are user/group specific (e.g., number of particles, etc.). 
???

## Inversion approach

The inversion method is the Hierarchical Bayesian Markov Chain Monte Carlo (HBMCMC) model (as described in Ganesan et al., 2014). The code is in open access on github : https://github.com/openghg/openghg_inversions (version ???).

### Model and measurement uncertainties

Use this section to describe uncertainties relating to the measurements and model, which apply to all species. 

- What measurement averaging time is used (if any)?
4 hours
- Are a subset of observations removed prior to the inversion. If so, what criteria are used (e.g., to remove measurements under stable conditions)? 
No
- How are measurement uncertainties used?
???
- How are model uncertainties estimated?
The model uncertainty is estimated with a uniform distibution (boundaries of 0.1 and 1) multiplied by the pollution event (expected distribution of the concentration derived from the emission distribution and the sensitivity matrix to the emissions, thus baseline removed) plus a minimum error term (fixed to 0.5).
- How are these different source of uncertainty combined?
They are aditionned and ???.
- How is the model compared to the observations? Sampled at same time/location? Comparison of monthly means? Spatially averaged? Are uncertainty covariances used? Etc. 
The model is compared to the observations using sampling at the same time and locations.

### Fluxes and uncertainties

- Over what time period are fluxes estimated (e.g., weekly, monthly). Note that this can be a scaling of a more finely time-resolved flux field. 
Monthly
- Describe any spatial basis function decomposition that is used. How are basis functions calculated ? 
We use 500 basis functions, calculated using a quadtree algorithm.
- What a priori uncertainty is assigned to each basis function? What prior PDF is used? 
The PDF used for the uncertainty is a truncated normal distribution. The mean of the used normal distribution is 1, the spread is 1 and the normal is truncated at 0, so to give non negative values.

### Boundary conditions

- How are boundary conditions or baselines prescribed or estimated? 
The baselines are estimated during the inversions. the input boundary conditions used as prior are coming from ??? CAMS version, ref ???.
- If estimated, what uncertainty is assigned to boundary conditions? 
To simulate the uncertainty in the boundary conditions, we use a truncated normal distribution. The mean of this distribution is 1, its spread 0.1 and its trucated at zero, so to give non negative values.

## References
Ganesan, A. L., Rigby, M., Zammit-Mangion, A., Manning, A. J., Prinn, R. G., Fraser, P. J., Harth, C. M., Kim, K.-R., Krummel, P. B., Li, S., Mühle, J., O'Doherty, S. J., Park, S., Salameh, P. K., Steele, L. P., and Weiss, R. F.: Characterization of uncertainties in atmospheric trace gas inversions using hierarchical Bayesian methods, Atmos. Chem. Phys., 14, 3855–3864, https://doi.org/10.5194/acp-14-3855-2014, 2014.

Eike H. Müller, Rupert Ford, Matthew C. Hort, Lois Huggett, Graham Riley, David J. Thomson, Parallelisation of the Lagrangian atmospheric dispersion model NAME, Computer Physics Communications, Volume 184, Issue 12, 2013, Pages 2734-2745, ISSN 0010-4655, https://doi.org/10.1016/j.cpc.2013.06.022.
