# RHIME inverse model specification

Transport model and inversion setup for the Univeristy of Bristol Regional Hierarchical Inverse Modelling Environment (RHIME). The following applies to all species, unless specified in a species-specific file in this folder.

## Transport model

NAME model (version 7.2) developped by the UK Met Office (Jones et al., 2007), a Langrangian particle model that we run backwards in time for each measurement site used in the inversion.

### Scope

- Domain: 10.73°N to 79.06°N and from 97.9°W to 39.38°E.
- Period: 2018-01-01 to 2023-01-01

### Meteorology

Meteorological fields from the UK Met Office Unified Model operational analyses are used. The model is run on a grid of horizontal resolution 0.141° x 0.0938° over the domain (Manning and Redington et al. 2021). Higher-resolution "UKV" meteorology is embedded within these fields over the UK and Ireland, with a resolution of 0.0135° x 0.0135°. Note that model "footprints" are stored at a coarser resolution than the meteorology (see below).

Vertically, there are 59 levels, from the surface to approximately 29km altitude.

### Model parameters

The transport model is used with a release of 20000 particles/hour. Particles are released from the inlet latitude and longitude, along a vertical line with a mid-point at the inlet height ± 20m (with a minimum release height of 0m). Particles are tracked for 30 days prior to the measurement, or until they leave the domain.

Particles are considered to interact with the surface when they are within 40m above the surface height. Footprints for each measurement are calculated for the time that the particles spend below this hight, integrated over the 30 day simulation.

Footprints are stored at a resolution of 0.352° longitude by 0.234°. Inversions are carried performed using a basis function decomposition of this output grid.

## Inversion approach

The inversion method is the Hierarchical Bayesian Markov Chain Monte Carlo (HBMCMC) model (as described in Ganesan et al., 2014). The code is in open access on github : https://github.com/openghg/openghg_inversions.

### Model and measurement uncertainties

The model is compared to the observations using 4h-averaged sampling at the same locations. Data are not included in the inversion when the planetary boundary layer height is less than 50m different from the inlet height.

The inversion is done by comparing the observation vector ($Y_{obs}$) to the simulated observations given by:

$$
Y_{\rm mod} = H_x x + H_{bc}x_{bc} + \epsilon
$$

where $H_x$ is a Jacobian matrix that quantifies the sensitivity of the mole fraction measurements to a *scaling* of the emissions field, $x$ is a vector of scaling factors. $H_{bc}$ is the sensitivity matrix for boundary conditions, $x_{bc}$ is the factor by which the boundary mole fraction is scaled for each of the cardinal directions (N, S, E, W). $\epsilon$ is the uncertainty associated with the observations and model:

$\epsilon = \max(\sqrt{\epsilon_{\rm meas}^2 + \epsilon_{\rm model}^2},\epsilon_{\rm min})$

The measurement uncertainty vector ($\epsilon_{\rm meas}$) contains a value for each element of $Y_{\rm obs}$, calculated as the standard deviation of the measurements over the averaging period. The model error ($\epsilon_{\rm model}$) is estimated for each site with scaling factors following uniform distibutions (boundaries of 0.1 and 1) multiplied by the mean simulated pollution event magnitude ($= H_x * x$). The minimum error ($\epsilon_{\rm min}$) is estimated using the standard deviation of $H_x x + H_{bc}x_{bc}-Y_{obs}$.

### Fluxes and uncertainties

The inversion scales fluxes within discrete spatial basis functions, calculated using a quadtree algorithm. The quadtree algorithm recursively splits the domain in smaller grid cells for regions which contribute the most to the *a priori* above basline mole fraction. This calculation is based on the average footprint over the inversion period and the a priori emissions field.

The PDF used for the flux uncertainties is a truncated normal distribution. The a priori emissions are multiplied by scaling factors following a normal distribution of mean 1, spread 1 and truncated at 0, so to give non negative values.

### Boundary conditions

Regional baselines are estimated by propagating to the site, 2D mole fraction fields at the domain edge. These boundary condition fields are obtained from global Eulerian model simulations or from some other estimate of the regional baseline mole fraction (e.g., Lunt et al., 2016).

A scaling of the boundary condition fields is solved for in the inversion. To simulate the uncertainty in the boundary conditions, we use a truncated normal distribution, obtained using a scaling factor. The mean of the distribution of the scaling factor is 1, its spread 0.1 and is truncated at zero, so to give non negative values.

## References
Ganesan, A. L., Rigby, M., Zammit-Mangion, A., Manning, A. J., Prinn, R. G., Fraser, P. J., Harth, C. M., Kim, K.-R., Krummel, P. B., Li, S., Mühle, J., O'Doherty, S. J., Park, S., Salameh, P. K., Steele, L. P., and Weiss, R. F.: Characterization of uncertainties in atmospheric trace gas inversions using hierarchical Bayesian methods, Atmos. Chem. Phys., 14, 3855–3864, https://doi.org/10.5194/acp-14-3855-2014, 2014.

Jones, A., Thomson, D., Hort, M., and Devenish, B.: The U. K. Met Office’s next-generation atmospheric dispersion model, NAME III, in: Air Pollution Modeling and its Application XVII, Proceedings of the 27th NATO/CCMS International Technical Meeting on Air Pollution Modelling and its Application, edited by: Borrego C. and Norman A.-L., Springer, 580–589, https://doi.org/10.1007/978-0-387-68854-1, 2007.

Lunt, M. F., Rigby, M., Ganesan, A. L., and Manning, A. J.: Estimation of trace gas fluxes with objectively determined basis functions using reversible-jump Markov chain Monte Carlo, Geoscientific Model Development, 9, 3213–3229, https://doi.org/10.5194/gmd-9-3213-2016, 2016.

Manning, A. J. and Redington, A. L. and Say, D. and O'Doherty, S. and Young, D. and Simmonds, P. G. and Vollmer, M. K. and M\"uhle, J. and Arduini, J. and Spain, G. and Wisher, A. and Maione, M. and Schuck, T. J. and Stanley, K. and Reimann, S. and Engel, A. and Krummel, P. B. and Fraser, P. J. and Harth, C. M. and Salameh, P. K. and Weiss, R. F. and Gluckman, R. and Brown, P. N. and Watterson, J. D. and Arnold, T. : Evidence of a recent decline in UK emissions of hydrofluorocarbons determined by the InTEM inverse model and atmospheric measurements, Atmospheric Chemistry and Physics, volume 21, number 16, pages 12739--12755, https://doi.org/10.5194/acp-21-12739-2021, 2021.
