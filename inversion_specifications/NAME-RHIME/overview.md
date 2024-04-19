# RHIME inverse model specification

This document is to describe features of the inverse modelling system, which is common to all gases. Species-specific features or modifications should be noted in the accompanying file for each species.

## Transport model

NAME model (version 7.2) developped by the UK Met Office (Muller et al. 2013) : it is a Langrangian particle model that we run backward in time. 

### Scope

- Domain (lon, lat range, or "global"): covering from 10.73N to 79.06N and from 97.9W to 39.38E.
- Period: 2018-01-01 to 2023-01-01

### Meteorology

The meteorological fields from the UK Met Office Unified Model are used. The model is run on a grid of horizontal resolution 0.352degree along longitude, 0.234degree along latitude. Vertically the grid goes from 500m to 19500m (center of cells?) with a vertical resolution of 1000m.

### Model input parameters

The langragian transport model is used with a release of 20000 particules/hour, and max number of particules set to 1e6. The sites and altitude used as input are described in the species specific files.

## Inversion approach

The inversion method is the Hierarchical Bayesian Markov Chain Monte Carlo (HBMCMC) model (as described in Ganesan et al., 2014). The code is in open access on github : https://github.com/openghg/openghg_inversions.

### Model and measurement uncertainties

The measurement are averaged on a four hour basis. We also remove the data for which the PBL height is less than 50m different from the inlet height.
- How are measurement uncertainties used?
???
- How are model uncertainties estimated?
The model uncertainties are estimated with scaling factors following uniform distibutions (boundaries of 0.1 and 1) multiplied by the pollution events (expected distribution of the concentration derived from the emission distribution and the sensitivity matrix to the emissions, thus baseline removed) plus a minimum error term (fixed to 0.5).
- How are these different source of uncertainty combined?
They are aditionned and ???.

The model is compared to the observations using 4h-averaged sampling at the same locations.

### Fluxes and uncertainties

The fluxes are estimated for each month.
We use 500 basis functions, calculated using a quadtree algorithm. The quadtree algorithm recursively splits the domain in smaller grid cells for regions which contribute more to the a priori (above basline) mole fraction. This is based on the average footprint over the inversion period and the a priori emissions field.

The PDF used for the fluxes uncertainties are truncated normal distributions. The a priori emissions are thus multiplied by scaling factors following a normal distribution of mean 1, spread 1 and truncated at 0, so to give non negative values.

### Boundary conditions

The baselines are estimated during the inversions. The input boundary conditions used as prior are coming from CAMS version 22, using Jungfraujoch monthly means as background. XXX don't know what that means XXX

To simulate the uncertainty in the boundary conditions, we use a truncated normal distribution, obtained using a scaling factor. The mean of the distribution of the scaling factor is 1, its spread 0.1 and its trucated at zero, so to give non negative values.

## References
Ganesan, A. L., Rigby, M., Zammit-Mangion, A., Manning, A. J., Prinn, R. G., Fraser, P. J., Harth, C. M., Kim, K.-R., Krummel, P. B., Li, S., Mühle, J., O'Doherty, S. J., Park, S., Salameh, P. K., Steele, L. P., and Weiss, R. F.: Characterization of uncertainties in atmospheric trace gas inversions using hierarchical Bayesian methods, Atmos. Chem. Phys., 14, 3855–3864, https://doi.org/10.5194/acp-14-3855-2014, 2014.

Eike H. Müller, Rupert Ford, Matthew C. Hort, Lois Huggett, Graham Riley, David J. Thomson, Parallelisation of the Lagrangian atmospheric dispersion model NAME, Computer Physics Communications, Volume 184, Issue 12, 2013, Pages 2734-2745, ISSN 0010-4655, https://doi.org/10.1016/j.cpc.2013.06.022.
