[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[NetworkCoding]] > [[HighwayNetworkCoding]]

***

This document is in need of update.  See old version at [[HighwayNetworkCoding_Old]]

Also see https://github.com/BayAreaMetro/travel-model-one/tree/master/utilities/check-network

Input network (freeflow.net) attributes:

| Variable | Description | Example |
|----------|-------------|---------|
| A | From node | 20298 |
| B | To node | 20300 |
| DISTANCE | Link Distance (miles) | 14.1 |
| SPDCLASS | Speed Class Type | 19 |
| CAPCLASS | Capacity Class Type | 19 |
| ROUTENUM | Highway number (e.g. 101, 880, 80, etc).  0 if not applicable. | 101 |
| ROUTEDIR | If ROUTENUM set, one of `N`,`S`,`E` or `W`.  Blank if not applicable. | N |
| AUX | ?? | 0 |
| YEAR | Year | 0 |
| FFS | Free Flow Speed | 60 |
| FFT | Free Flow Time | 14.1 |
| FT2000 | Facility Type in Year 2000 | 2 |
| GL | County Code. 1=San Francisco; 2=San Mateo; 3=Santa Clara; 4=Alameda; 5=Contra Costa; 6=Solano; 7= Napa; 8=Sonoma; 9=Marin; 10=external | 4 |
| LANES | Number of Lanes | 2 |
| AT | [Area Type](https://github.com/BayAreaMetro/modeling-website/wiki/MasterNetworkLookupTables#area-type-at) | 2 |
| FT | [Facility type](https://github.com/BayAreaMetro/modeling-website/wiki/MasterNetworkLookupTables#facility-type-ft)  | 2 |
| TOLLCLASS | [Toll Code](https://github.com/BayAreaMetro/modeling-website/wiki/MasterNetworkLookupTables#toll-code-tollclass) | 0 |
| USE | [Vehicle restrictions](https://github.com/BayAreaMetro/modeling-website/wiki/MasterNetworkLookupTables#vehicle-restrictions-use) | 1 |
| BRT | [Bus Rapid Transit](https://github.com/BayAreaMetro/modeling-website/wiki/MasterNetworkLookupTables#bus-rapid-transit-brt) | 0 |
| TOS | [Traffic Operations](https://github.com/BayAreaMetro/modeling-website/wiki/MasterNetworkLookupTables#traffic-operations-tos) | 0 |
| SIGCOR | [Arterial Signal Coordination](https://github.com/BayAreaMetro/modeling-website/wiki/MasterNetworkLookupTables#arterial-signal-coordination-sigcor) | 0 |
| OT | Observed Time for Toll Queuing Links | 0 |

*Table 6 Highway Network Calculated Link Attributes*

| Variable | Description | Example |
|----------|-------------|---------|
| METER | Ramp meter present, set If(FT2000=8) | 1 |
| FT | Facility type modified IF (FT=8) FT=5 | 2 |
| FT2000 | Facility type in year 2000 modified IF (FT2000=8) FT2000=5 | 2 |
| CAPCLASS | Capacity class type, set by [AT](MasterNetworkLookupTables), [FT](MasterNetworkLookupTables), [TOS](MasterNetworkLookupTables) and SIGCOR type lookup | 19 |
| FFS | Free flow speed, set by CAPCLASS | 60 |
| CAP | Capacity per lane, set by CAPCLASS | 1950 |
| FFT | Free flow time, calculated as (DISTANCE/FFS)*60 or as OT, IF(TSIN=1 & TOLLCLASS=1-100) | 14.1 |
| OT | Observed time, set to FFT If(TSIN=1 & TOLLCLASS=0) | 3.5 |
 
