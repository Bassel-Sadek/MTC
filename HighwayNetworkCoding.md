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
| GL | County Code | 4 |
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
 

*Table 7 Input and Output Files of Network_Update_Modified.job*

| Input/Output | Description | Example |
|--|--|--|
| I | Project Specific Highway Network | Year2040_Base_NETWORK_December22_2010_w.NET |
| O | Output Updated Project Specific Highway Network | Year2040_Base_NETWORK_December22_2010.NET |

## 4. Creating Highway Networks by Time of Day

After creating the project specific network file, the analyst must create the highway network files by time-of-day. This is done in two stages:
1. The analyst adds five sets of toll values to each link in the network where each set represents one of the five time periods shown in Table 8 and each set includes toll values for each user class.
1. The analyst runs the script to create five highway networks by time-of-day.

All tolls should be expressed in year 2000 cents. The scripts to do these two steps are: [SetTolls.job](HighwayNetworkCoding#41-script-settollsjob) followed by [CreateFiveHighwayNetworks.job](HighwayNetworkCoding#42-script-createfivehighwaynetworksjob).

*Table 8 Highway Network Time Periods*

| &lt;timeperiod&gt;Code | Name | Hours |
|--|--|--|
| EA | Early AM | 3am to 6am |
| AM | AM Peak Period | 6am to 10am |
| MD | Midday | 10am to 3pm |
| PM | PM Peak Period | 3pm to 7pm |
| EV | Evening | 7pm to 3am |


### 4.1 Script "SetTolls.job"

Before creating the time-of-day networks, but after creating the project-specific network, the analyst then updates the bridge and value tolls. Bridge tolls are the tolls charged at the bridges and value tolls are tolls paid to save time by shifting to an alternative facility (e.g. HOT) or nearby facility. Each of the eight existing Bay Area bridge toll booths links has a unique TOLL coded as shown in Table 9. All tolls should be expressed in year 2000 cents. To change a toll value, the script must be changed.

*Table 9 Bay Area Bridge Toll Class*

| Toll Class Code | Bay Area Bridge | Example |
|--|--|--|
| 1 | Benicia-Martinez Bridge | If (A = 11597 & B = 11683) TOLL = 0 |
| 2 | Carquinez Bridge | If (A = 11667 & B = 11634) TOLL = 0 |
| 3 | Richmond Bridge | If (A = 2341 & B = 2357) TOLL = 0 |
| 4 | Golden Gate Bridge | If (A = 7319 & B = 7338) TOLL = 0 |
| 5 | San Francisco/ Oakland Bay Bridge | If (A = 2784 & B = 2802) TOLL = 0 |
| 6 | San Mateo Bridge | If (A = 3642 & B = 3649) TOLL = 0 |
| 7 | Dumbarton Bridge | If (A = 3895 & B = 3896) TOLL = 0 |
| 8 | Antioch Bridge | If (A = 1673 & B = 1621) TOLL = 0 |
| 9* | Reserved for New Bridges |   |
| 10* | Reserved for New Bridges |   |
| 11* | Reserved for Value tolls which are used by HOT lanes and are defined in hwyParam.block |   |

*Note that Toll Classes 9-11 are reserved for new bridges and test case scenarios.

The attribute TOLL is a legacy attribute and is no longer output by this script. Instead, TOLL is set first, then a new attribute TOLLCLASS is set to TOLL. The attribute TOLLCLASS then becomes the output. A separate toll can be specified for each vehicle class. The vehicle class link toll link attributes are shown in Table 10. A separate toll can be specified for each vehicle class, as shown in Table 11. Table 12 shows the inputs and outputs of this script.

*Table 10 Toll User Class Specific Link Attributes*

| &lt;userclass&gt;Code | Description | Example |
|--|--|--|
| DA | Drive alone, SOV | 200 |
| S2 | Shared ride two, HOV2 | 150 |
| S3 | Shared ride three plus, HOV3+ | 100 |
| VSM | Very small commercial trucks, which are assumed to be two-axle vehicles | 100 |
| SML | Small commercial trucks, which are assumed to be two-axle vehicles | 100 |
| MED | Medium commercial trucks, which are assumed to be three-axle vehicles | 100 |
| LRG | Combination trucks, which are charged the average of the five- and six-axle fee | 100 |


*Table 11 Output Toll Class Link Attributes*

| Variable | Description | Example |
|--|--|--|
| TOLL&lt;timeperiod&gt;_&lt;userclass&gt; | Bridge and Value Tolls by User Class and Time of Day | TOLLEA_DA = 200 |
| TOLLCLASS | Replaces TOLL values with TOLLCLASS | TOLLCLASS = TOLL |


*Table 12 Input and Output Files from this Script*

| Input/Output | Description | Example |
|--|--|--|
| I | Updated Project Specific highway Network | freeflow.net |
| O | Highway Network with Toll values | withTolls.net |

