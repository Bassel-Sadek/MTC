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
 
## Arterial Signal Coordination (SIGCOR)

| SIGCOR | Definition |
|-----|------------|
| 0 | Signals on the roadway segment are <em>not </em>coordinated |
| 1 | Signals on the roadway segment are coordinated |

## Vehicle Restrictions (USE)

| USE | Definition |
|-----|------------|
| 1 | All vehicles may use the roadway |
| 2 | High-occupancy vehicle (HOV) lane with a minimum of two persons per vehicle; combination trucks prohibited |
| 3 | High-occupancy vehicle (HOV) lane with a minimum of three persons per vehicle; combination trucks prohibited |
| 4 | Combination trucks prohibited |

## Toll Code (TOLLCLASS)

| TOLLCLASS | Definition |
|-----|------------|
| 1 | Code specific to the Benicia-Martinez Bridge (prices then set in SetTolls.job script) |
| 2 | Code specific to the Carquinez Bridge |
| 3 | Code specific to the Richmond-San Rafael Bridge |
| 4 | Code specific to the Golden Gate Bridge |
| 5 | Code specific to the San Francisco-Oakland Bay Bridge |
| 6 | Code specific to the San Mateo-Hayward Bridge |
| 7 | Code specific to the Dumbarton Bridge |
| 8 | Code specific to the Antioch Bridge |
| 9 | Placeholder for future bridge and/or cordon toll codes |
| 10 | Placeholder for future bridge and/or cordon toll codes |
| 11 and higher | Codes specific to high-occupancy toll (HOT) roadway segments |

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

The formula is as follows:  (total population + 2.5 * total employment) / (developed residential acres + developed commercial acres)

| AT | Label | Range |
|----|-------|-------|
| 0 | Regional core | &gt; 300 |
| 1 | Central business district | 100 to 300 |
| 2 | Urban business<span style="white-space: pre;"> </span> | 55 to 100 |
| 3 | Urban | 30 to 55 |
| 4 | Suburban | 6 to 30 |
| 5 | Rural | &lt; 6 |

 
## Bus Rapid Transit (BRT)

| BRT | Definition |
|-----|------------|
| 0 | Roadway segment does _not_ include a dedicated bus lane with full BRT treatments |
| 1 | Roadway segment includes a dedicated bus lane with full BRT treatments |
