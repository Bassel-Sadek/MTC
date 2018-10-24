[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[LoadedHighway]]

---

A "loaded" roadway network is the result of the travel model's systematic assignment of all vehicles to paths, or routes. The variables input to this process are described in [[HighwayNetworkCoding]] and [[MasterNetworkLookupTables]]; variables output from this process are described below. Note that this single loaded network represents a conflation of five time-of-day specific networks. As such, certain time-of-day specific network parameters (such as the USE code) which are included in this network do not represent the condition of the network across all five times of day.

The token **XX** in the variable names below represents a two-letter time-of-day string for which the variable is specific. Values of XX include "24hr", which identifies daily quantities as well as each of the travel model's [[TimePeriods]] two-letter codes.

The token **YYY** is a two-or-three letter string indicating the vehicle class in the assignment. Values of **YYY** are as follows:
* DA, for single-occupant passenger vehicles ("drive alone") that decide _not_ to pay an HOT-lane fee;
* DAT, for single-occupant passenger vehicles that decide to pay an HOT lane-fee;
* S2, for two-occupant passenger vehicles ("shared ride 2") that decide _not_ to pay an HOT-lane fee;
* S2T, for two-occupant passenger vehicles that decide to pay an HOT-lane fee;
* S3, for three-or-more-occupant passenger vehicles ("shared ride 3+") that decide _not_ to pay an HOT-lane fee;
* S3T, for three-or-more occupant passenger vehicles that decide to pay an HOT-lane fee;
* SM, for very small (four-tire two-axle), small (six-tire two-axle), and medium (three-axle) commercial vehicles that decide <em>not </em>to pay an HOT-lane fee;
* SMT, for very small, small, and medium commercial vehicles that decide to pay an HOT-lane fee;
* HV, for large, combination (four-axle or more) commercial vehicles that decide <em>not </em>to pay an HOT-lane fee;
* HVT, for large, combination commercial vehicles that decide to pay an HOT-lane fee.

To view the network in a GIS software package, use the following projection: UTM NAD 1983 ZONE 10N. [[See example arcpy code here.|https://github.com/BayAreaMetro/travel-model-one/commit/7958ae09449c7a2c33fa6851fc4a0ac6dec25fa4]]

| Name | Definition | Scale |
|---|---|---|
| CTIM**XX** | Congested travel time (time-of-day specific) | Minutes, Float, 0 and up |
| CSPD**XX** | Congested travel speed (time-of-day specific) | Miles per hour, Float 0 and up |
| VC**XX** | Volume-to-capacity ratio (time-of-day specific) | Ratio, Float, 0 and up |
| VOL**XX**_**YYY** | Vehicle volume (time-of-day and vehicle-class specific) | Vehicles, Float, 0 and up |
| DELAY**XX** | Link-specific delay, which is the difference between the congested travel time and the free flow travel time (time-of-day specific) | Vehicle Hours, Float, 0 and up |
| VMT**XX** | Link-specific vehicle-miles traveled, which is the link volume times the link distance (time-of-day specific) | Vehicle-miles, Float, 0 and up |
| VHT**XX** | Link-specific vehicle-hours traveled, which is the link volume times the link travel time (time-of-day specific) | Vehicle-hours, Float, 0 and up |
 

-- Main.DavidOry - 24 Jun 2011