[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[InputFiles]]

***

The table below contains brief descriptions of the input files required to execute the MTC travel model.

| File name | Purpose | Folder Location | File type | File format |
|-----------|---------|-----------------|-----------|-------------|
| freeflow.NET | Highway network | hwy\ | [Citilabs Cube](http://citilabs.com/products/cube) | [[HighwayNetworkCoding]] |
| tazData.csv | Travel analysis zone-specific data | landuse\ | CSV | [[TazData]] |
| tazData.dbf | Travel analysis zone-specific data | landuse\ | DBF | [[TazData]] |
| walkAccessBuffers. float.csv | Walk access shares | landuse\ | CSV | [[WalkAccessBuffers]] |
| truckFF.dat | Friction factors for the commercial vehicle distribution models | nonres\ | ASCII | [[TruckDistribution]] |
| truckkfact. k22.z1454.mat | "K-factors" for the commercial vehicle distribution models | nonres\ | [Citilabs Cube](http://citilabs.com/products/cube) | [[TruckDistribution]] |
| ixDailyx4.tpp | Internal-external fixed trip table | nonres\ | [Citilabs Cube](http://citilabs.com/products/cube) | [[FixedDemand]] |
| tripsAirPax**XX**.tpp | Airport passenger fixed trip table (**XX** is the [[TimePeriods]] code) | nonres\ | [Citilabs Cube](http://citilabs.com/products/cube) | [[FixedDemand]] |
| ixex_config.dbf | Interregional commercial travel assumptions | nonres\ | DBF | [[TazData]] |
| hhFile. **XXXX**.**YYYY**.csv | Synthetic population household file (**XXXX** denotes the forecast series from which the data is derived; **YYYY** denotes the forecast year) | popsyn\ | CSV | [[PopSynHousehold]] |
| personFile. **XXXX**.**YYYY**.csv | Synthetic population person file (**XXXX** denotes the forecast series from which the data is derived; **YYYY** denotes the forecast year) | popsyn\ | CSV | [[PopSynPerson]] |
| Various | Myriad transit files used to define the transit network and service | trn\ | Various | [[TransitNetworkCoding]] |
| trips**XX**.tpp | Warm start passenger trip tables (**XX** is the [[TimePeriods]] code) | warmstart\ main | [Citilabs Cube](http://citilabs.com/products/cube) | As output by the travel model |
| tripsIx**XX**.tpp | Warm start internal external trip tables (**XX** is the [[TimePeriods]] code) | warmstart\ nonres | [Citilabs Cube](http://citilabs.com/products/cube) | As output by the travel model |
| tripsTrk**XX**.tpp | Warm start commercial vehicle trip tables (**XX** is the [[TimePeriods]] code) | warmstart\ nonres | [Citilabs Cube](http://citilabs.com/products/cube) | As output by the travel model |
| tripsAirPax**XX**.tpp | Warm start air passenger trip tables (**XX** is the [[TimePeriods]] code) | warmstart\ nonres | [Citilabs Cube](http://citilabs.com/products/cube) | [[FixedDemand]] |

-- Main.DavidOry - 21 Jan 2012