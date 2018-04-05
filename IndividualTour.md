[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[IndividualTour]]

---

Simulation results specific to individual tour decisions.

| Name | Definition | Scale | Join with &hellip; |
|---|---|---|---|
| hh_id | Unique household ID number | Long integer, any value | All model files, [synthetic population household file](PopSynHousehold) |
| person_id | Unique person ID number | Long integer, any value | [Synthetic population person file](PopSynPerson), [[Person]] |
| person_num | Person number unique to the household | Integer, 1 to household size | [[Person]] |
| person_type | Person lifestage/employment type | Integer, 1 - Full-time worker; 2 - Part-time worker; 3 - University student; 4 - Nonworker; 5 - Retired; 6 - Student of non-driving age; 7 - Student of driving age; 8 - Child too young for school |   |
| tour_id | Individual tour number unique to the person | Integer, 0 (1 individual tour), 1, 2, 3, or 4 (5 individual tours) |   |
| tour_category | Type of tour | String, "MANDATORY"; "INDIVIDUAL_NON_MANDATORY"; "AT_WORK" |   |
| tour_purpose | Tour purpose, given the type of tour | String, "work_low"; "work_med"; "work_high"; "work_very high"; "university"; "school_high"; "school_grade"; "atwork_business"; "atwork_eat"; "atwork_maint"; "eatout"; "escort_kids"; "escort_no kids"; "othdiscr", "othmaint"; "shopping"; "social" |   |
| orig_taz | Origin transportation analysis zone | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| orig_walk_segment | Walk to transit origin sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit |   |
| dest_taz | Destination transportation analysis zone | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| dest_walk_segment | Walk to transit destination sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit |   |
| start_hour | Start time of the tour | Integer, 5 to 23, where 5 is the hour from 5 am to 6 am and 23 is the hour from 11 pm to midnight |   |
| end_hour | End time of the tour | Integer, 5 to 23, where 5 is the hour from 5 am to 6 am and 23 is the hour from 11 pm to midnight |   |
| tour_mode | Primary (though not necessarily used) travel mode for the tour | Integer, 1 - Drive alone free; 2 - Drive alone pay; 3 - Shared ride 2 free; 4 - Shared ride 2 pay; 5 - Shared ride 3+ free; 6 - Shared ride 3+ pay; 7 - Walk; 8 - Bike; 9 - Walk to local bus; 10 - Walk to light rail or ferry; 11 - Walk to express bus; 12 - Walk to BART; 13 - Walk to commuter rail; 14 - Drive to local bus; 15 - Drive to light rail or ferry; 16 - Drive to express bus; 17 - Drive to BART; 18 - Drive to commuter rail |   |
| atWork_freq | Number of at work sub-tours (non-zero only for work tours) | Integer |   |
| num_ob_stops | Number of out-bound stops on the tour (from home for all tours except at work; from work for at work tours) | Integer |   |
| num_ib_stops | Number of in-bound stops on the tour (to home for all tours except at work; to work for at work tours) | Integer |   |


-- Main.DavidOry - 07 Jun 2011