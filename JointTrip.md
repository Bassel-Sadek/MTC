[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[JointTrip]]

---

Simulation results specific to joint trip decisions. Joint travel is defined in the model structure as two or more individuals from the same household making a complete travel tour together.

| Name | Definition | Scale | Join with &hellip; |
|---|---|---|---|
| hh_id | Unique household ID number | Long integer, any value | All model files, [synthetic population household file](PopSynHousehold) |
| tour_id | Joint tour number unique to the household | Integer, 0 or 1 (0 represents first joint tour, 1 represents the second if there are two) | [[JointTour]] |
| stop_id | Stop number unique to half tour | Integer, in order of trips; -1 if this is a half tour |   |
| inbound | Inbound stop indicator | Dummy, 1 if the stop is on the inbound leg of the tour, 0 otherwise |   |
| tour_purpose | Purpose of the joint tour | String, "eatout", "othdiscr", "othmaint", "shopping", "social" |   |
| orig_purpose | Purpose at the origin end of the trip | String, "Home", "eatout", "othdiscr", "othmaint", "shopping", "social" |   |
| dest_purpose | Purpose at the destination end of the trip | String, "Home", "eatout", "othdiscr", "othmaint", "shopping", "social" |   |
| orig_taz | Origin transportation analysis zone | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| orig_walk_segment | Walk to transit origin sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit |   |
| dest_taz | Destination transportation analysis zone | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| dest_walk_segment | Walk to transit destination sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit |   |
| parking_taz | Transportation analysis zone in which the trip maker(s) park (model component not yet implemented) | Integer, 1 to 1454; 0 if no parking zone is selected |   |
| depart_hour | Time of departure for the trip | Integer, 5 to 23, where 5 is the hour from 5 am to 6 am and 23 is the hour from 11 pm to midnight |   |
| trip_mode | Travel mode for the trip | Integer, see [[TravelModes#tour-and-trip-modes]] |   |
| num_participants | Number of participants on the tour | Integer, 2 and up |   |
| tour_mode | Primary (though not necessarily used) travel mode for the tour | Integer, see [[TravelModes#tour-and-trip-modes]] |   |
| tour_category | Tour category<span style="white-space: pre;"> </span> | String, "JOINT_NON_MANDATORY" |   |
 


-- Main.DavidOry - 22 Apr 2014