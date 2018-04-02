[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[IndividualTrip]]

---

Simulation results specific to individual trip decisions.

| Name | Definition | Scale | Join with &hellip; |
|---|---|---|---|
| hh_id | Unique household ID number | Long integer, any value | All model files, [synthetic population household file](PopSynHousehold) |
| person_id | Unique person ID number | Long integer, any value | [Synthetic population person file](PopSynPerson), [[Person]] |
| person_num | Person number unique to the household | Integer, 1 to household size | [[Person]] |
| tour_id | Individual tour number unique to the person | Integer, 0 (1 individual tour), 1, 2, 3, or 4 (5 individual tours), or, for at work sub-tours, a two-digit integer where the first digit is the individual tour number (1-based) and the second digit is the sub-tour number (e.g. 12, is second sub-tour made on tour number 1, which has a tour_id of 0). | [[IndividualTour]] |
| stop_id | Stop number unique to half tour | Integer, in order of trips; -1 if this is a half tour |   |
| inbound | Inbound stop indicator | Dummy, 1 if the trip is on the inbound leg of the tour, 0 otherwise |   |
| tour_purpose | Tour purpose, given the type of tour | String, "work_low"; "work_med"; "work_high"; "work_very high"; "university"; "school_high"; "school_grade"; "atwork_business"; "atwork_eat"; "atwork_maint"; "eatout"; "escort_kids"; "escort_no kids"; "othdiscr", "othmaint"; "shopping"; "social" |   |
| orig_purpose | Purpose at the origin end of the trip | String, "Home", "work_low"; "work_med"; "work_high"; "work_very high"; "university"; "school_high"; "school_grade"; "atwork_business"; "atwork_eat"; "atwork_maint"; "eatout"; "escort_kids"; "escort_no kids"; "othdiscr", "othmaint"; "shopping"; "social" |   |
| dest_purpose | Purpose at the destination end of the trip | String, "Home", "work_low"; "work_med"; "work_high"; "work_very high"; "university"; "school_high"; "school_grade"; "atwork_business"; "atwork_eat"; "atwork_maint"; "eatout"; "escort_kids"; "escort_no kids"; "othdiscr", "othmaint"; "shopping"; "social" |   |
| orig_taz | Origin transportation analysis zone | Integer, 1 to 1454 | [Shape file](http://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f#visualize) |
| orig_walk_segment | Walk to transit origin sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short walk to transit; 2 - long walk to transit |   |
| dest_taz | Destination transportation analysis zone | Integer, 1 to 1454 | [Shape file](http://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f#visualize) |
| dest_walk_segment | Walk to transit destination sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short walk to transit; 2 - long walk to transit |   |
| parking_taz | Transportation analysis zone in which the trip maker(s) park (model component not yet implemented) | Integer, 1 to 1454; 0 if no parking zone is selected |   |
| depart_hour | Time of departure for the trip | Integer, 5 to 23, where 5 is the hour from 5 am to 6 am and 23 is the hour from 11 pm to midnight |   |
| trip_mode | Travel mode for the trip | Integer, 1 - Drive alone free; 2 - Drive alone pay; 3 - Shared ride 2 free; 4 - Shared ride 2 pay; 5 - Shared ride 3+ free; 6 - Shared ride 3+ pay; 7 - Walk; 8 - Bike; 9 - Walk to local bus; 10 - Walk to light rail or ferry; 11 - Walk to express bus; 12 - Walk to BART; 13 - Walk to commuter rail; 14 - Drive to local bus; 15 - Drive to light rail or ferry; 16 - Drive to express bus; 17 - Drive to BART; 18 - Drive to commuter rail |   |
| tour_mode | Primary (though not necessarily used) travel mode for the tour | Integer, 1 - Drive alone free; 2 - Drive alone pay; 3 - Shared ride 2 free; 4 - Shared ride 2 pay; 5 - Shared ride 3+ free; 6 - Shared ride 3+ pay; 7 - Walk; 8 - Bike; 9 - Walk to local bus; 10 - Walk to light rail or ferry; 11 - Walk to express bus; 12 - Walk to BART; 13 - Walk to commuter rail; 14 - Drive to local bus; 15 - Drive to light rail or ferry; 16 - Drive to express bus; 17 - Drive to BART; 18 - Drive to commuter rail |   |
| tour_category | The type of tour for which this trip is a part | String, "AT_WORK", "INDIVIDUAL_NON_MANDATORY", "MANDATORY", |   |

-- Main.DavidOry - 07 Jun 2011