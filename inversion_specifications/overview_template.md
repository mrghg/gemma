# {INVERSION SYSTEM NAME} inverse model specification

This document is to describe features of the inverse modelling system, which is common to all gases. Species-specific features or modifications should be noted in the accompanying file for each species.

## Transport model

Brief overview of transport model, including appropriate references.

### Scope

- Domain (lon, lat range, or "global"):
- Period: 

### Meteorology

- Which meteorological fields are used?
- What resolution(s) is the model being run at (include any interpolation of the met. fields, and any difference between model transport and output resolutions)?

## Inversion approach

Describe the inversion approach. If described in publication(s), provide appropriate references. If not described elsewhere, provide full details here.

### Model and measurement uncertainties

Use this section to describe uncertainties relating to the measurements and model, which apply to all species. 

- What measurement averaging time is used (if any)?
- Are a subset of observations removed prior to the inversion. If so, what criteria are used (e.g., to remove measurements under stable conditions)?
- How are measurement uncertainties used?
- How are model uncertainties estimated?
- How are these different source of uncertainty combined?
- How is the model compared to the observations? Sampled at same time/location? Comparison of monthly means? Spatially averaged? Etc.

### Fluxes and uncertainties

- Over what time period are fluxes estimated (e.g., weekly, monthly). Note that this can be a scaling of a more finely time-resolved flux field.
- Describe any spatial basis function decomposition that is used. How are basis functions calculated?
- What a priori uncertainty is assigned to each basis function? What prior PDF is used?

### Boundary conditions

- How are boundary conditions or baselines prescribed or estimated?
- If estimated, what uncertainty is assigned to boundary conditions?