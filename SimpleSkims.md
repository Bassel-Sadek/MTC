[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[SimpleSkims]]

---

Three sets -- [time](SimpleSkims#time-skims), [distance](SimpleSkims#distance-skims), [cost](SimpleSkims#cost-skims) -- of simplified level-of-service matrices, referred to as "skims", are described here. Each set contains five time-of-day specific comma-separated values files, corresponding to the five time periods considered in the travel model, as follows: (1) early AM, 3 am to 6 am (EA); (2) AM peak period, 6 am to 10 am (AM); (3) midday, 10 am to 3 pm (MD); (4) PM peak period, 3 pm to 7 pm (PM); and, (5) evening, 7 pm to 3 am the next day (EV).

If travel between two points by the mode in question is not possible (or highly unlikely, e.g. a transit trip that would take 5 hours), the skim data contains a value of -999. 

## Time Skims

For automobile travel, the time includes the network time plus the terminal time (the time needed to move from the automobile to the destination location); the transit time reflects the best path (in which all transit modes are considered) for each of the three access/egress combinations (walk-transit-walk, drive-transit-walk, and walk-transit-drive), with intra-zonal time missing (the mode choice model does not allow intra-zonal transit travel); and, the bicycle and walk times are based on assumed travel speeds (12 mph and 3 mph respectively, which are the same values used in the mode choice models) and the distance is based on the roadway network (with freeways and certain bridges removed). Time units are minutes.

| Name | Definition | Join with &hellip; |
|---|---|---|
| orig | Origin transportation analysis zone | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| dest | Destination transportation analysis zone | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| da | Door-to-door time for the drive alone travel mode (i.e. single occupant private automobile) |   |
| daToll | Door-to-door time for the drive alone value toll travel mode (those willing to pay to use an HOT lane) |   |
| s2 | Door-to-door time for the shared ride 2 travel mode (i.e. double occupant private automobile) |   |
| s2Toll | Door-to-door time for the shared ride 2 value toll travel mode (those willing to pay to use an HOT lane) |   |
| s3 | Door-to-door time for the shared ride 3+ travel mode (i.e. three-or-more occupants traveling in a private vehicle) |   |
| s3Toll | Door-to-door time for the shared ride 3+ value toll travel mode (those willing to pay to use an HOT lane, if scenario policy dictates they must pay) |   |
| walk | Door-to-door time for walking |   |
| bike | Door-to-door time for bicycling |   |
| wTrnW | Door-to-door time for walk to transit to walk paths |   |
| dTrnW | Door-to-door time for drive to transit to walk paths |   |
| wTrnD | Door-to-door time for walk to transit to drive paths (returning home on a park-and-ride tour) |   |


## Distance Skims

For automobile travel, the distance includes the centroid-to-centroid network distance; transit distance is not skimmed and, as such, not included; and, the bicycle and walk distances are based on the centroid-to-centroid roadway network distances (with freeways and certain bridges removed). Distance units are miles.

| Name | Definition | Join with &hellip; |
|---|---|---|
| orig | Origin transportation analysis zone | [Shape file](http://opendata.mtc.ca.gov/datasets/travel-analysis-zones) |
| dest | Destination transportation analysis zone | [Shape file](http://opendata.mtc.ca.gov/datasets/travel-analysis-zones) |
| da | Distance for the drive alone travel mode (i.e. single occupant private automobile) |   |
| daToll | Distance for the drive alone value toll travel mode (those willing to pay to use an HOT lane) |   |
| s2 | Distance for the shared ride 2 travel mode (i.e. double occupant private automobile) |   |
| s2Toll | Distance for the shared ride 2 value toll travel mode (those willing to pay to use an HOT lane) |   |
| s3 | Distance for the shared ride 3+ travel mode (i.e. three-or-more occupants traveling in a private vehicle) |   |
| s3Toll | Distance for the shared ride 3+ value toll travel mode (those willing to pay to use an HOT lane, if scenario policy dictates they must pay) |   |
| walk | Distance for walking |   |
| bike | Distance for bicycling |   |


## Cost Skims

For automobile travel, the cost includes bridge tolls, value (HOT-lane) tolls, and an assumed scenario-specific per mile operating cost; the two- and three-plus-occupancy automobile travel cost is scaled to distribute the costs to each traveler; the transit cost includes the transit fare; and, bicycle and walk travel are assumed to be free. Cost units are cents, expressed in year 2000 dollars.

| Name | Definition | Join with &hellip; |
|---|---|---|
| orig | Origin transportation analysis zone | [Shape file](http://opendata.mtc.ca.gov/datasets/travel-analysis-zones) |
| dest | Destination transportation analysis zone | [Shape file](http://opendata.mtc.ca.gov/datasets/travel-analysis-zones) |
| da | Cost for the drive alone travel mode (i.e. single occupant private automobile) |   |
| daToll | Cost for the drive alone value toll travel mode (those willing to pay to use an HOT lane) |   |
| s2 | Cost for the shared ride 2 travel mode (i.e. double occupant private automobile) |   |
| s2Toll | Cost for the shared ride 2 value toll travel mode (those willing to pay to use an HOT lane) |   |
| s3 | Cost for the shared ride 3+ travel mode (i.e. three-or-more occupants traveling in a private vehicle) |   |
| s3Toll | Cost for the shared ride 3+ value toll travel mode (those willing to pay to use an HOT lane, if scenario policy dictates they must pay) |   |
| wTrnW | Cost for walk to transit to walk paths |   |
| dTrnW | Cost for drive to transit to walk paths |   |
| wTrnD | Cost for walk to transit to drive paths (returning home on a park-and-ride tour) |   | 

-- Main.DavidOry - 24 Oct 2014