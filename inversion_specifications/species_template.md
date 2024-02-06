# {INVERSION SYSTEM NAME} specification for CH4

Use this file to provide any species-specific inversion specifications, or modifications to the general approach outined in the overview.

## Scope (optional)

- Domain (optional, lon, lat): 
- Time period: 

## Fluxes

List of flux datasets, including any modifications:

- {Flux dataset 1}
  - Reference:
  - Native spatial resolution:
    - Regridded to (optional, include method + software): 
  - Native temporal resolution:
    - Resampled to: (optional, include method): 

### Basis function decomposition (optional)

Describe the basis function decomposition, if different to that specified in inversion system overview.

### Flux uncertainty (optional)

Describe the flux uncertainty, if different to that specified in inversion system overview. Over what time resolution are fluxes solved for (weekly, monthly, etc.)?

## Observations

Provide an obspack reference, if used. Otherwise, state which measurements have been used.

- Obspack reference: (optional)

Or:

- {Network 1}:
  - Reference:
  - Sites: A, B, C
  - 

Describe any modification to the observations, including:
- Removal of a subset of observations, if not described in the overview (describe criteria)
- Averaging/resampling

### Measurement/model uncertainty (optional)

Describe measurement/model uncertainty, if different to the overview.

How is the model compared to the observations? Sampled at same time/location? Comparison of monthly means? Spatially averaged? Etc.

## Boundary conditions (optional)

- Boundary condition reference (include version number): 
- 