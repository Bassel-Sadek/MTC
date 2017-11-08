[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[LoadedTransit]]

---

A "loaded" transit netowrk is the result of the travel model's systematic assignment of all transit riders to specific paths and routes. The variables input to this process are described in the TransitNetworkCoding section. Transit results are summarized by link and by line. The transit link data is rather difficult to work with as the transit network is complex. The transit line data is much easier to work with and summarized here.

The travel model performs seventy-five independent transit assignments. To do so, MTC first segments both supply and demand by time-of-day (using these TimePeriods). In each of these time periods, demand is segmented into three access/egress categories, as follows:

1. Walk to transit, walk from transit (or walk-transit-walk), abbreviated WLK_**XXX**_WLK  in the PATH ID field, where **XXX** is the path category abbreviation presented below;
1. Drive to transit, walk from transit (or walk-transit-drive), abbreviated DRV_**XXX**_WLK;
1. Walk to transit, drive from transit (or walk-transit-drive), abbreviated WLK_**XXX**_DRV.

And, finally, separate bundles of transit services are packaged together to create different types of transit options for travelers to choose among. In the MTC application, supply within each time period and demand within each time period and each access/egress category, is segmented into one of the following five path categories:
1. Local bus service only (see the [[TransitModes]] page for the transit options defined as "local bus"), abbreviated _LOC_ in the PATH ID field;
1. Local bus, _light rail, and ferry service_, abbreviated _LRF_;
1. Local bus, light rail, ferry, and _express bus service_, abbreviated _EXP_;
1. Local bus, light rail, ferry, express bus, and _heavy rail service_, abbreviated _HVY_; and,
1. Local bus, light rail, ferry, express bus, heavy rail, and _commuter rail service_ (all transit modes), abbreviated _COM_.
The travel model generates demand estimates by time of day, access/egress category, and path category. Five time categories times three access/egress categories times five path categories results in a total of seventy-five assignment results.


| Name | Definition | Scale |
|---|---|---|
| NAME | The text name assigned to each transit route. The prefix of the name typically denotes the line's TransitMode. Note that each route pattern is designated as a separate line. | String |
| MODE | Mode of this specific line (a complete list of [[TransitModes]] is available here) | Integer, 1 and up |
| OWNER | Intended to be the designated operating agency; it is not used consistently by MTC | N/A |
| FREQUENCY | Headway of this service during this time interval (e.g. a value of 15 means a transit vehicle arrives at every point on its route every 15 minutes) | Minutes, Float, 1 to 99.99 |
| LINE TIME | Time it takes a transit vehicle to traverse the route | Minutes, Float, 0.0 and up |
| LINE DIST | Route distance | Miles, Float, 0.0 and up |
| TOTAL BOARDINGS | Route-level boardings for this time-of-day/access-egress/path combination | Integer, 0 and up |
| PASSENGER MILES | Number of passenger miles (one passenger on the route for one mile is one passenger mile) | Float, 0.0 and up |
| PASSENGER HOURS | Number of passenger hours (one passenger on the route for 30 minutes is one-half passenger hour) | Float, 0.0 and up |
| PATH ID | Code identifying the demand segment in the form **TT_ACC_PTH_EGR**, where **TT** is the [[TimePeriods]] abbreviation; **ACC** and **EGR** are the access/egress abbreviations; and **PTH** is the three-letter path abbreviation | String |
 

-- Main.DavidOry - 13 Jan 2012