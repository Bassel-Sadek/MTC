[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[Household]]

---

# Household results from Travel Model

Household-specific results from the travel model simulation.

| Name | Definition | Scale | Join with &hellip; |
|---|---|---|---|
| hh_id | Unique household ID number | Integer, any value | All model files, <a href="/foswiki/bin/view/Main/PopSynHousehold" target="_blank" title="Household file from Population Synthesizer">synthetic population household file</a> |
| taz | Transportation analysis zone of home location | Integer, 1 to 1454 | <a href="https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f" target="_blank" title="TAZ map">Shape file</a> |
| walk_subzone | Walk to transit sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit |   |
| income | Annual household income ($2000) | Integer, 0 and up |   |
| autos | Household automobiles | Integer |   |
| jtf_choice | Number and type of household joint tours | Integer, -4 - no joint tours, only pre-school children leave household; -3 - no joint tours, fewer than 2 people leave household; -2 - no joint tours, single person hh; 1 - no joint tours; 2 - 1 shop (S); 3 - 1 maintenance (M); 4 - 1 eating out (E); 5 - 1 visiting family/friends (V); 6 - 1 discretionary (D); 7 - 2 shop (SS); 8 - 1 shop, 1 maintenance (SM); 9 - 1 shop, 1 eating out (SE); 10 - 1 shop, 1 visit (SV); 11 - 1 shop, 1 discretionary (SD); 12 - 2 maintenance (MM); 13 - 1 maintenance, 1 eating out (ME); 14 - 1 maintenance, 1 visit (MV); 15 - 1 maintenance, 1 discretionary (MD); 16 - 2 eating out; 17 - 1 eating out, 1 visit (EV); 18 - 1 eating out, 1 discretionary (ED); 19 - 2 visiting; 20 - 1 visit, 1 discretionary; 21 - 2 discretionary |   |
| size | Number of persons in the household | Integer, 1 and up |   |
| workers | Number of full- or part-time workers in the household | Integer, 0 and up |   |
| auto_suff | Incorrectly coded; ignore<span style="white-space: pre;"> </span> |   |   |
| ao_rn | Random number for automobile ownership model | Integer, any value |   |
| fp_rn | Random number for free parking model | Integer, any value |   |
| cdap_rn | Random number for coordinated daily activity pattern model | Integer, any value |   |
| imtf_rn | Random number for individual mandatory tour frequency model | Integer, any value |   |
| imtod_rn | Random number for individual mandatory tour time-of-day model | Integer, any value |   |
| immc_rn | Random number for individual mandatory mode choice model | Integer, any value |   |
| jtf_rn | Random number for joint tour frequency model | Integer, any value |   |
| jtl_rn | Random number for joint tour location choice model | Integer, any value |   |
| jtod_rn | Random number for joint tour time-of-day model | Integer, any value |   |
| jmc_rn | Random number for joint tour mode choice model | Integer, any value |   |
| inmtf_rn | Random number for individual non-mandatory tour frequency model | Integer, any value |   |
| inmtl_rn | Random number for individual non-mandatory location choice model | Integer, any value |   |
| inmtod_rn | Random number for individual non-mandatory time-of-day model | Integer, any value |   |
| inmmc_rn | Random number for individual non-mandatory mode choice model | Integer, any value |   |
| awf_rn | Random number for at-work frequency model | Integer, any value |   |
| awl_rn | Random number for at-work location choice model | Integer, any value |   |
| awtod_rn | Random number for at-work time-of-day model | Integer, any value |   |
| awmc_rn | Random number for at-work mode choice model | Integer, any value |   |
| stf_rn | Random number for stop frequency model | Integer, any value |   |
| stl_rn | Random number for stop location choice model | Integer, any value |   |
| humanVehicles | Household automobiles, human-driven. [(New in TM1.5)](https://github.com/BayAreaMetro/modeling-website/wiki/TravelModel1.5#Model_Outputs) | Integer, 0 and up | |
| autonomousVehicles | Household automobiles, autonomous. [(New in TM1.5)](https://github.com/BayAreaMetro/modeling-website/wiki/TravelModel1.5#Model_Outputs) | Integer, 0 and up | |
 
