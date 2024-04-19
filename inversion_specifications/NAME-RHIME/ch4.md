# RHIME specification for CH4

Use this file to provide any species-specific inversion specifications, or modifications to the general approach outined in the overview.

## Fluxes

List of flux datasets, including any modifications:

- EDGAR combined with UKGHG for UK.
  - Reference:
    - EDGAR version 8 : European Union 2023, European Commission, Joint Research Centre (JRC), EDGAR (Emissions Database for Global Atmospheric Research) Community GHG database, comprising IEA-EDGAR CO2, EDGAR CH4, EDGAR N2O and EDGAR F-gases version 8.0 (2023)
    - UKGHG inventory for the year 2019.
  - Native spatial resolution: 0.1degree x 0.1degree for EDGAR, 1km x 1km for UKGHG
    - Regridded to : 0.35degree along longitude, 0.23degree along latitude.
  - Native temporal resolution: monthly
    - Resampled to: yearly

## Observations

- ICOS:
  - Reference:
  - Sites: 'BIR','BRM','CBW','CMN',
        'GAT','HEI','HEL','HPB',
        'HTM','HUN','JFJ','KIT','KRE',
        'LIN','LUT','MHD','NOR','OPE',
        'OXK','PAL','SAC','SMR',
        'SSL','STE','TOH','TRN',
        'UTO','WAO','WES'
    - Inlet heights : '75magl','212magl','207magl','8magl',
        '341magl','30magl','110magl','131magl',
        '150magl','115magl',None,'200magl','250magl',
        '98magl','60magl','24magl','100magl','120magl',
        '163magl','12magl','100magl','125magl',
        '12magl','252magl','147magl','180magl',
        '57magl','10magl','14magl'
- DECC:
  - Reference:
  - Sites: 'BSD','HFD','RGL','TAC',
  - Inlet heights : '248magl','100magl','90magl','185magl',

Modification to the observations:
- Already descibed in overview.md
