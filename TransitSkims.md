[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[TransitSkims]]

The [transit skimming procedure](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/scripts/skims/TransitSkims.job) creates skim tables for five time periods, three access/egress combinations, and six line-haul mode combinations. 

The five time periods are: (i) early AM, before 6 am; (ii) AM peak period, 6 am to 10 am; (iii) midday, 10 am to 3 pm; (iv) PM peak period, 3 pm to 7 pm; and (v) evening, after 7 pm. 

The three access/egress combinations are: (i) walk/transit/walk; (ii) drive/transit/walk; and (iii) walk/transit/drive. 

The six line-haul mode combinations are: (i) long-haul premium or commuter rail; (ii) medium-haul premium or heavy rail (BART) (iii) medium-haul basic or express bus; (iv) short-haul premium or light rail; (v) short-haul basic or local bus; and (vi) a generic transit path used to calculate accessibility.

Note that ferry is included in the short-haul premium or light rail line-haul options.  This was done to reduce the number of skims that need to be created.  Because light rail and ferry do not compete with each other, travelers in corridors with light rail are presented with the light rail choice and travelers in corridors with ferry are presented with the ferry choice. 

The procedure outputs a 16-table skim for each time-of-day, access/egress, and line-haul mode combination, containing the following:
|Name	|Definition|	Notes|
|---|---|---|
|ivt	|Transit in-vehicle time, time (minutes x 100)|	
|iwait	|Initial wait time, time (minutes x 100)|	
|xwait	|Transfer wait time, time (minutes x 100)	
|wacc	|Walk access time (mode 1), time (minutes x 100)|	Walk from centroid to auxiliary rail node/bus stop|
|waux	|Auxiliary walk time (modes 3, 4, and 5), time (minutes x 100)|	Transfer between walk auxiliary node and station platform node|
|wegr	|Walk egress time (mode 6), time (minutes x 100)|	Walk from auxiliary rail node/bus stop to centroid|
|dtime	|Drive access and/or egress time (modes 2 or 7), time (minutes x 100)|	
|ddist	|Drive access and/or egress distance (modes 2 or 7), distance (miles x 100)|	
|fare	|Fare, cents (2000$)|	
|boards	|Boardings, number|	
|ivtLOC	|Local bus in-vehicle time (modes 10 through 79), time (minutes x 100)|	
|ivtLRF	|Light rail and/or ferry in-vehicle time (modes 100 through 119), time (minutes x 100)|	
|ivtEXP	|Express bus in-vehicle time (modes 80 through 99), time (minutes x 100)|	
|ivtHVY	|Heavy rail in-vehicle time (modes 120 through 129), time (minutes x 100)|	
|ivtCOM	|Commuter rail in-vehicle time (modes 130 through 139), time (minutes x 100)|	
|ivtFerry	|Ferry in-vehicle time (modes 100 through 109), time (minutes x 100)|	

A complete list of transit mode definitions can be found in [[TransitModes]].

More information about walk access time, walk egress time and auxiliary walk time can be found in [[TransitNetworkCoding]].
