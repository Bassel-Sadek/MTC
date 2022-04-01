[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[TransitSkims]]

# Background

The [transit skimming procedure](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/scripts/skims/TransitSkims.job) creates skim tables for five time periods, three access/egress combinations, and six line-haul mode combinations. 

The five time periods are: (i) early AM, before 6 am; (ii) AM peak period, 6 am to 10 am; (iii) midday, 10 am to 3 pm; (iv) PM peak period, 3 pm to 7 pm; and (v) evening, after 7 pm. 

The three access/egress combinations are: (i) walk/transit/walk; (ii) drive/transit/walk; and (iii) walk/transit/drive. 

The six line-haul mode combinations are: (i) long-haul premium or commuter rail; (ii) medium-haul premium or heavy rail (BART) (iii) medium-haul basic or express bus; (iv) short-haul premium or light rail or ferry; (v) short-haul basic or local bus; and (vi) a generic transit path used to calculate accessibility.

Some notes on the line-haul mode combinations:
-  **Light rail and ferry are grouped together.**  This was done to reduce the number of skims that need to be created.  Because light rail and ferry do not compete with each other, travelers in corridors with light rail are presented with the light rail choice and travelers in corridors with ferry are presented with the ferry choice. 

-** What is the "generic transit path"? **The generic skims are used by [Accessibility.job](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/scripts/skims/Accessibility.job) to create skims/accessibility.csv which is used by the auto ownership model. They do not necessarily represent the best transit impedance for each OD; they represent paths found in which all line-haul modes are treated equally i.e. having equal mode-specific perceived time factors. In comparison, the non-generic line-haul mode skims have mode-specific perceived time factors that are set to be lower for the given line-haul mode than other line-haul modes. The example below, which is an excerpt of TransitSkims.job, compares mode-specific perceived time factors for the generic “all transit treated equally” mode to “local bus” mode.

Generic TRN mode example:

`; all transit treated equally`

`; mode-specific perceived time factors` 

`; support loc bus exp bus ferry lt rail hvy rail com rail`

`token_modefac = 'modefac = 9*2.0, 70*1.0, 20*1.0, 10*1.0, 10*1.0, 10*1.0, 10*1.0'`

The mode-specific perceived time factors are same (1.0) for all mode all modes, except for support (access/egress/transfer) which is 2.0.

Local bus example:

`; local bus or short-haul basic;` 

`; mode-specific perceived time factors`

`;  support  loc bus  exp bus   ferry  lt rail  hvy rail  com rail`

`token_modefac = 'modefac  =   9*2.0,  70*1.0,  20*1.5, 10*1.5,  10*1.5,   10*1.5,   10*1.5'`   

The mode-specific perceived time factor for local bus is 1, and they are higher for other modes.

# Definitions
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
