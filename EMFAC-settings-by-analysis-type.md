[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[EMFAC settings]]

***

This document is work in progress. 

Related documentation that exists now: https://github.com/BayAreaMetro/modeling-website/wiki/EmissionFactors

EMFAC settings for different types of analysis for MTC:
|EMFAC GUI Screen |   Selection category |   Options |   Type of analysis |    |    |   
|----------|-------------|---------|
| |    |    |   SB375 emfac prep |   AQ conformity |   EIR |   RTP Development
|1 |   Run Mode |   Emissions |   x |   x |   x |   x
| |    |   Emissions Rates |    |    |    |   x
| |   Run Type |   Default Activity |    |    |    |   
| |    |   Custom Activity |   x |   x |   x |   x
| |   Generate template or load file |   Generate Custom Activity Template |   x |   x |   x |   x
| |    |   Load Custom Activity File |   x |   x |   x |   
| |    |   Input Emission Rate Parameters |    |    |    |   x
|2 |   Area |   Sub-Area |   Includes the entire 9 counties in the region |   Nonattainment Area/SF Air Basin only [excludes northern Sonoma and eastern Solano] |   Nonattainment Area/SF Air Basin only [excludes northern Sonoma and eastern Solano] |   |Includes the entire 9 counties in the region
|3 |   Calendar Year |   2000 to 2050 |   pick the analysis year |   Horizon year of RTP plus interim years [no more than 10 years apart] |   Horizon year of RTP plus Base year |   Horizon year of RTP plus Base year
| |   Season/ Month |   Season |   Annual |   Summer and Winter |   Summer, Winter and Annual |   Summer, Winter and Annual
| |    |   Month |   N/A |   N/A |   N/A |   N/A
|4 |   VMT Data Type |   Total Daily VMT |    |   x |   x |   x
| |    |   VMT by Vehicle and Fuel Type |   x |    |    |   
| |    |   Custom Hourly Speed Fractions |   x |   x |   x |   x





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