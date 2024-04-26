# RHIME inverse model specification

Transport model and inversion setup for the Univeristy of Bristol Regional Hierarchical Inverse Modelling Environment (RHIME). The following applies to all species, unless specified in a species specific file in this folder.

## Transport model

NAME model (version 7.2) developped by the UK Met Office (Muller et al. 2013), a Langrangian particle model that we run backwards in time for each measurement site used in the inversion.

### Scope

- Domain: 10.73°N to 79.06°N and from 97.9°W to 39.38°E.
- Period: 2018-01-01 to 2023-01-01

### Meteorology

The meteorological fields from the UK Met Office Unified Model are used. The model is run on a grid of horizontal resolution 0.0135° x 0.0135° over the UK (Manning and Redington et al. 2021). Vertically, it uses 57 levels, expanding to 12.2km.

### Model input parameters

The langragian transport model is used with a release of 20000 particles/hour. Particles are released from the measurement altitude ± X m. Particles are tracked for 30 days prior to the measurement, or until they leave the domain.

## Inversion approach

The inversion method is the Hierarchical Bayesian Markov Chain Monte Carlo (HBMCMC) model (as described in Ganesan et al., 2014). The code is in open access on github : https://github.com/openghg/openghg_inversions.

### Model and measurement uncertainties

The measurement are averaged on a four hour basis. We also remove the data for which the PBL height is less than 50m different from the inlet height.

The inversion is done by comparing the observation vector ($Y_{obs}$) to the simulated observations given by:

$$
Y_{mod} = H_x x + H_{bc}x_{bc} + \epsilon
$$

where Hx is the sensitivity matrix that maps emissions to measurement, x is the emission vector (prior emissions multiplied by scaling factor), Hbc is the sensitivity matrix that maps boundary conditions to measurement, xbc is the boundary conditions vector (prior boundary conditions multiplied by a scaling factor) and epsilon the term representing the error : epsilon = sqrt(meas_error ** 2 + model_error ** 2 + min_error ** 2). The measurement uncertainty vector (meas_err) contains a value for each element of Yobs (i.e. each site), calculated as the standard deviation of the measurements over the averaging period. The model error (model_error) is estimated for each site with scaling factors following uniform distibutions (boundaries of 0.1 and 1) multiplied by the pollution events (= Hx * x, which is the expected distribution of the concentration derived from the emission distribution and the sensitivity matrix to the emissions, thus baseline removed). The minimum error is arbitrarly fixed with a value specific for each gases.

The model is compared to the observations using 4h-averaged sampling at the same locations.

### Fluxes and uncertainties

The inversion scales fluxes within discrete spatial basis functions, calculated using a quadtree algorithm. The quadtree algorithm recursively splits the domain in smaller grid cells for regions which contribute the most to the *a priori* above basline mole fraction. This calculation is based on the average footprint over the inversion period and the a priori emissions field.

The PDF used for the flux uncertainties is a truncated normal distribution. The a priori emissions are multiplied by scaling factors following a normal distribution of mean 1, spread 1 and truncated at 0, so to give non negative values.

### Boundary conditions

The baselines are estimated during the inversions. The input boundary conditions used as priors are the monthly means of the observations at Jungfrauhoch, unless otherwise stated.

To simulate the uncertainty in the boundary conditions, we use a truncated normal distribution, obtained using a scaling factor. The mean of the distribution of the scaling factor is 1, its spread 0.1 and is truncated at zero, so to give non negative values.

## References
Ganesan, A. L., Rigby, M., Zammit-Mangion, A., Manning, A. J., Prinn, R. G., Fraser, P. J., Harth, C. M., Kim, K.-R., Krummel, P. B., Li, S., Mühle, J., O'Doherty, S. J., Park, S., Salameh, P. K., Steele, L. P., and Weiss, R. F.: Characterization of uncertainties in atmospheric trace gas inversions using hierarchical Bayesian methods, Atmos. Chem. Phys., 14, 3855–3864, https://doi.org/10.5194/acp-14-3855-2014, 2014.

Eike H. Müller, Rupert Ford, Matthew C. Hort, Lois Huggett, Graham Riley, David J. Thomson, Parallelisation of the Lagrangian atmospheric dispersion model NAME, Computer Physics Communications, Volume 184, Issue 12, 2013, Pages 2734-2745, ISSN 0010-4655, https://doi.org/10.1016/j.cpc.2013.06.022.

Manning, A. J. and Redington, A. L. and Say, D. and O'Doherty, S. and Young, D. and Simmonds, P. G. and Vollmer, M. K. and M\"uhle, J. and Arduini, J. and Spain, G. and Wisher, A. and Maione, M. and Schuck, T. J. and Stanley, K. and Reimann, S. and Engel, A. and Krummel, P. B. and Fraser, P. J. and Harth, C. M. and Salameh, P. K. and Weiss, R. F. and Gluckman, R. and Brown, P. N. and Watterson, J. D. and Arnold, T. : Evidence of a recent decline in UK emissions of hydrofluorocarbons determined by the InTEM inverse model and atmospheric measurements, Atmospheric Chemistry and Physics, volume 21, number 16, pages 12739--12755, https://doi.org/10.5194/acp-21-12739-2021, 2021.
