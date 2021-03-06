[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[NetworkCoding]] > [[MasterNetworkLookupTables]]

---

Definition of variables included in the master network.
* [Traffic Operations (TOS)](MasterNetworkLookupTables#traffic-operations-tos)
* [Arterial Signal Coordination (SIGCOR)](MasterNetworkLookupTables#arterial-signal-coordination-sigcor)
* [Vehicle Restrictions (USE)](MasterNetworkLookupTables#vehicle-restrictions-use)
* [Toll Code (TOLLCLASS)](MasterNetworkLookupTables#toll-code-tollclass)
* [Facility Type (FT)](MasterNetworkLookupTables#facility-type-ft)
* [Area Type (AT)](MasterNetworkLookupTables#area-type-at)
* [Bus Rapid Transit (BRT)](MasterNetworkLookupTables#bus-rapid-transit-brt)


## Traffic Operations (TOS)

| TOS | Definition |
|-----|------------|
| 0 | Freeway is _not_ managed with ramp metering infrastructure |
| 1 | Freeway is managed with ramp metering infrastructure |
| 2 | Freeway is managed with ramp metering and other (tbd) infrastructure |

## Arterial Signal Coordination (SIGCOR)

| SIGCOR | Definition |
|-----|------------|
| 0 | Signals on the roadway segment are <em>not</em> coordinated |
| 1 | Signals on the roadway segment are coordinated |

## Vehicle Restrictions (USE)

| USE | Definition |
|-----|------------|
| 1 | All vehicles may use the roadway |
| 2 | High-occupancy vehicle (HOV) lane with a minimum of two persons per vehicle; combination trucks prohibited |
| 3 | High-occupancy vehicle (HOV) lane with a minimum of three persons per vehicle; combination trucks prohibited |
| 4 | Combination trucks prohibited (used for Express Lanes) |

## Toll Code (TOLLCLASS)

| TOLLCLASS | Definition | Opening Year (or anticipated) for toll collection | Source (2015 Base or NetworkProject) |
|-----|------------|-----|-----|
| 1 | Code specific to the Benicia-Martinez Bridge | [1962](https://en.wikipedia.org/wiki/Benicia%E2%80%93Martinez_Bridge#Historical_toll_rates)| 2015 Base |
| 2 | Code specific to the Carquinez Bridge | [1958](https://en.wikipedia.org/wiki/Carquinez_Bridge#Historical_toll_rates) | 2015 Base |
| 3 | Code specific to the Richmond-San Rafael Bridge | [1956](https://en.wikipedia.org/wiki/Richmond%E2%80%93San_Rafael_Bridge#Historical_toll_rates) | 2015 Base |
| 4 | Code specific to the Golden Gate Bridge | [1937](https://en.wikipedia.org/wiki/Golden_Gate_Bridge#Tolls) | 2015 Base |
| 5 | Code specific to the San Francisco-Oakland Bay Bridge | [1936](https://en.wikipedia.org/wiki/San_Francisco%E2%80%93Oakland_Bay_Bridge#Financing_and_tolls) | 2015 Base |
| 6 | Code specific to the San Mateo-Hayward Bridge | [1929](https://en.wikipedia.org/wiki/San_Mateo%E2%80%93Hayward_Bridge#Historical_toll_rates) | 2015 Base |
| 7 | Code specific to the Dumbarton Bridge | [1927](https://en.wikipedia.org/wiki/Dumbarton_Bridge_(California)#Historical_toll_rates) | 2015 Base |
| 8 | Code specific to the Antioch Bridge | [1978](https://en.wikipedia.org/wiki/Antioch_Bridge#Historical_toll_rates) | 2015 Base |
| 9 | Code specific to the Treasure Island Congestion Pricing | [2035](https://app.asana.com/0/741988522701299/928782229623106) | 2015 Base |
| 10 | Code specific to the San Francisco Congestion Pricing (Cordon Toll) | [2025](https://archive.sfcta.org/sites/default/files/content/Planning/CongestionPricingFeasibilityStudy/PDFs/MAPS_study_final_lo_res.pdf) | 2015 Base |
| 11 and higher | Codes specific to high-occupancy toll (HOT) roadway segments and/or cordon tolls | | |
| 231 | [SR-237 Express Lanes Phase 1](https://511.org/driving/express-lanes/b-sr-237-express-lanes) - SR237 - US101 Interchange to I-880 Interchange - EB | Mar 2012 | 2015 Base |
| 232 | [SR-237 Express Lanes Phase 1](https://511.org/driving/express-lanes/b-sr-237-express-lanes) - SR237 - US101 Interchange to I-880 Interchange - WB | Mar 2012 | 2015 Base |
| 690 | [I-680 Sunol Express Lane](https://511.org/driving/express-lanes/i-680-sunol-express-lane) - I-680 ALA - SCL County Line to SR84 - SB | Sep 2010 | 2015 Base |
| 887 | [SR-237 Express Lanes Phase 1](https://511.org/driving/express-lanes/b-sr-237-express-lanes) - I-880 SCL - SR237 to SR262 Mission Blvd - NB (last segment after TOLLCLASS 231) | Mar 2012 | 2015 Base |
| 888 | [SR-237 Express Lanes Phase 1](https://511.org/driving/express-lanes/b-sr-237-express-lanes) - I-880 SCL - SR237 to SR262 Mission Blvd - SB (first segment before TOLLCLASS 232) | Mar 2012 | 2015 Base |

## Facility Type (FT)

| FT | Definition |
|-----|------------|
| 1 | Freeway-to-freeway connector |
| 2 | Freeway |
| 3 | Expressway |
| 4 | Collector |
| 5 | Freeway ramp |
| 6 | Dummy link |
| 7 | Major arterial |
| 8 | Managed Freeway |
| 9 | Special facility |
| 10 | Toll plaza |

## Area Type (AT)

The formula is as follows: ??(total population + 2.5 * total employment) / (developed residential acres + developed commercial acres)

| AT | Label | Range |
|----|-------|-------|
| 0 | Regional core | &gt; 300 |
| 1 | Central business district | 100 to 300 |
| 2 | Urban business<span style="white-space: pre;"> </span> | 55 to 100 |
| 3 | Urban | 30 to 55 |
| 4 | Suburban | 6 to 30 |
| 5 | Rural | &lt; 6 |
| 6 | Not an area type, this is added to enable a special capclass 62 for I280 in TM1.5| NA |
??
## Bus Rapid Transit (BRT)

| BRT | Definition |
|-----|------------|
| 0 | Roadway segment does _not_ include a dedicated bus lane with full BRT treatments |
| 1 | Roadway segment includes a dedicated bus lane with full BRT treatments |
| 2 | Roadway segment includes reduced bus delays (e.g. transit signal priority) |
| 3 | Roadway segment (freeway) allows for buses to travel on the shoulder |

The BRT attribute is used in [PrepHwyNet.job](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/scripts/skims/PrepHwyNet.job#L138)