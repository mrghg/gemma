# GEOS-Chem-EnKF specification for CO2

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

- {Biomas burning GFAS v1.2 inventory }
- Reference: Kaiser et al., 2012: htps://doi.org/10.5194/bg-9-527-2012
  - Native spatial resolution: 0.1° x 0.1°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: daily 
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

- {Ocean fluxes, the NEMO-PISCES model} 
- Reference: Lefèvre et al., 2020: https://doi.org/10.1016/j.jmarsys.2020.103419
  - Native spatial resolution: 0.25° x 0.25°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: monthly
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

- {Lateral carbon fluxes related to crop removal}
- Reference: Deng et al., 2022: https://doi.org/10.5194/essd-14-1639-2022
  - Native spatial resolution: 0.08333° x 0.08333°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: yearly 
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

- {Terrestrial biosphere fluxes, the VPRM model}
- Reference: Gerbig 2021: https://doi.org/10.18160/R9X0-BW7T
  - Native spatial resolution: 1/120° x 1/60°
    - Regridded to 0.25° x 0.3125° 
  - Native temporal resolution: hourly
    - Resampled to: converted to kg/m2/s using the model time step (done inside the GEOS-Chem model)

## Observations

Provide an obspack reference, if used. Otherwise, state which measurements have been used.

- ICOS (~ 50 sites availble for the model domain, PAL is not within the modelling domain):
   - Obspack reference: 
      Multi-laboratory compilation of atmospheric carbon dioxide data for
      the period 1957-2022; obspack_co2_1_GLOBALVIEWplus_v9.1_2023-12-08;
      NOAA Earth System Research Laboratory, Global Monitoring Laboratory.
      http://doi.org/10.25925/20231201

- DECC:
  - Reference:
  - Sites: 'BSD','HFD','RGL','TAC',;
  - Inlet heights : '248magl','100magl','90magl','185magl';

Describe any modification to the observations, including:
- Removal of a subset of observations, if not described in the overview (describe criteria)
- Averaging/resampling

We keep only well-mixed atmosphere when the standard deviation of concentrations within the lowest 5 vertical levels (top ~ 600 m) in the model is < 5 ppm
See the rest details in [the overview](./overview.md).

### Measurement/model uncertainty (optional)

Describe measurement/model uncertainty, if different to the overview.

The model uncertainty, including atmospheric transport error, is set to 3 ppm.
See the rest details in [the overview](./overview.md)