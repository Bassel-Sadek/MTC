[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[JointTour]]

---

Simulation results specific to joint tour decisions. Joint travel is defined in the model structure as two or more individuals from the same household making a complete travel tour together.

| Name | Definition | Scale | Join with &hellip; |
|---|---|---|---|
| hh_id | Unique household ID number | Long integer, any value | All model files, [synthetic population household file](PopSynHousehold) |
| tour_id | Joint tour number unique to the household | Integer, 0 or 1 (0 represents first joint tour, 1 represents the second if there are two) | [Synthetic population person file](PopSynPerson), Model files specific to persons and individual travel |
| tour_category | Type of joint tour | String, "JOINT_NON_MANDATORY", which is the only type of joint tour currently modeled |   |
| tour_purpose | Purpose of the joint tour | String, "eatout", "othdiscr", "othmaint", "shopping", "social" |   |
| tour_composition | Type of tour composition | Integer, 1 - adults only; 2 - children only; 3 - adults and children |   |
| tour_participants | Household members participating in the tour | String of Integers, with spaces between, of the person_num | [Person file](Person) |
| orig_taz | Origin transportation analysis zone | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| orig_walk_segment | Walk to transit origin sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit |   |
| dest_taz | Destination transportation analysis zone | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| dest_walk_segment | Walk to transit destination sub-zone (not located in space) | Integer, 1 to 1454 |   |
| start_hour | Start time of the tour | Integer, 5 to 23, where 5 is the hour from 5 am to 6 am and 23 is the hour from 11 pm to midnight |   |
| end_hour | End time of the tour | Integer, 5 to 23, where 5 is the hour from 5 am to 6 am and 23 is the hour from 11 pm to midnight |   |
| tour_mode | Primary (though not necessarily used) travel mode for the tour | Integer, 1 - Drive alone free; 2 - Drive alone pay; 3 - Shared ride 2 free; 4 - Shared ride 2 pay; 5 - Shared ride 3+ free; 6 - Shared ride 3+ pay; 7 - Walk; 8 - Bike; 9 - Walk to local bus; 10 - Walk to light rail or ferry; 11 - Walk to express bus; 12 - Walk to BART; 13 - Walk to commuter rail; 14 - Drive to local bus; 15 - Drive to light rail or ferry; 16 - Drive to express bus; 17 - Drive to BART; 18 - Drive to commuter rail |   |
| num_ob_stops | Number of out-bound (from home) stops on the tour | Integer, 0 and up |   |
| num_ib_stops | Number of in-bound (to home) stops on the tour | Integer, 0 and up |   |
 

-- Main.DavidOry - 07 Jun 2011