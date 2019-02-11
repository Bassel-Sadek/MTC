[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[TravelModes]]

***

The MTC travel model defines twenty-three unique ways in which a traveler can move across the roadway and/or transit networks.

Automobile travelers are explicitly assigned to occupancy and toll eligibility classes. The toll eligibility class decision determines whether those traveling in the vehicle are willing to pay (a so-called value toll) to travel on a faster parallel or nearly parallel route, such as in a high occupancy toll (HOT) facility. The toll eligibility class does not determine a willingness to pay a toll to cross a bridge.

Transit travelers are explicitly assigned to a specific transit line. As a simplification, MTC groups transit lines by the following technology categories: local bus, express bus, light rail, ferry, heavy rail, and commuter rail. Local bus transit service represents standard, fixed-route bus service, of the kind a traveler may take to and from a neighborhood grocery store, as well as bus rapid transit service. Express bus service represents longer-distance service typically provided in over-the-road coach technology; Golden Gate Transit, for example, provides this service between Marin County and downtown San Francisco. Light rail service is represented in the Bay Area by San Franciscos Muni Metro and F-Market streetcar services, as well as Santa Clara Valley Transportation Authoritys light rail service. Heavy rail service is provided in the Bay Area by the Bay Area Rapid Transit (BART) district. Finally, commuter rail captures longer distance rail service typically on grade-separated railroads; Caltrain, for example, offers this service along the Peninsula (other Bay Area providers of commuter rail service are Altamont Commuter Express and Amtrak). The detailed services that make up each of these technology categories is available on the [[TransitModes]] page.

Transit travelers are presented up to 10 path options when deciding how to get from A to B. As a convenience, these 10 options are created by excluding certain technologies. The first path option includes only the local bus modes and, as such, are labeled local bus; the second includes local bus, light rail, and ferry modes and is labeled light rail/ferry; the third includes local bus, light rail, ferry, and express bus modes and is labeled express bus; the fourth includes local bus, light rail, ferry, express bus, and heavy rail modes and is labeled heavy rail; and, finally, the fifth includes all of the transit modes and is labeled commuter rail. If a traveler has their car with them, he/she are presented the walk/transit/walk options as well as the drive/transit/walk path options; if the traveler left home making a drive/transit/walk trip, he/she are presented, for all subsequent trips before returning home, the walk/transit/walk options as well as the walk/transit/drive options. Defining path choices in this way provides MTC a convenient framework for organizing transit behavior.

| Number | Name | Label(s) |
|---|----|---|
| 1 | Drive alone (single-occupant vehicles), <em>not </em>eligibile to use value toll facilities | DA |
| 2 | Drive alone (single-occupant), eligible to use value toll facilities | DATOLL |
| 3 | Shared ride 2 (two-occupant vehicles), <em>not </em>eligibile to use value toll facilities | SR2 |
| 4 | Shared ride 2 (two-occupant vehicles), eligible to use value toll facilities | SR2TOLL |
| 5 | Shared ride 3+ (three-or-more-occupant vehicles), <em>not </em>eligibile to use value toll facilities | SR3 |
| 6 | Shared ride 3+ (three-of-more occupant vehicles), eligible to use value toll facilities | SR3TOLL |
| 7 | Walk the entire way (no transit, no bicycle) | WALK |
| 8 | Bicycle the entire way (no transit) | BIKE |
| 9 | Walk access, local bus, walk egress | WLK_LOC_WLK |
| 10 | Walk access, light rail or ferry, walk egress | WLK_LRF_WLK |
| 11 | Walk access, express bus, walk egress | WLK_EXP_WLK |
| 12 | Walk access, heavy rail, walk egress | WLK_HVY_WLK |
| 13 | Walk access, commuter rail, walk egress | WLK_COM_WLK |
| 14 | Drive access, local bus, walk egress | DRV_LOC_WLK |
| 15 | Drive access, light rail or ferry, walk egress | DRV_LRF_WLK |
| 16 | Drive access, express bus, walk egress | DRV_EXP_WLK |
| 17 | Drive access, heavy rail, walk egress | DRV_HVY_WLK |
| 18 | Drive access, commuter rail, walk egress | DRV_COM_WLK |
| 19 | Walk access, local bus, drive egress | WLK_LOC_DRV |
| 20 | Walk access, light rail or ferry, drive egress | WLK_LRF_DRV |
| 21 | Walk access, express bus, drive egress | WLK_EXP_DRV |
| 22 | Walk access, heavy rail, drive egress | WLK_HVY_DRV |
| 23 | Walk access, commuter rail, drive egress | WLK_COM_DRV |
| 24 | Drive alone, TNC | da_tnc |
| 25 | Shared ride 2, TNC | sr2_tnc |
| 26 | Shared ride 3+, TNC | sr3_tnc |
| 27 | Drive alone, owned autonomous vehicle (AV) | da_av |
| 28 | Shared ride 2, owned autonomous vehicle (AV) | sr2_av |
| 29 | Shared ride 3+, owned autonomous vehicle (AV) | sr3_av |
 
## Tour and Trip Modes

| Number | Name |
|---|----|
| 1 | Drive alone (single-occupant vehicles), <em>not </em>eligibile to use value toll facilities |
| 2 | Drive alone (single-occupant), eligible to use value toll facilities |
| 3 | Shared ride 2 (two-occupant vehicles), <em>not </em>eligibile to use value toll facilities |
| 4 | Shared ride 2 (two-occupant vehicles), eligible to use value toll facilities |
| 5 | Shared ride 3+ (three-or-more-occupant vehicles), <em>not </em>eligibile to use value toll facilities |
| 6 | Shared ride 3+ (three-of-more occupant vehicles), eligible to use value toll facilities |
| 7 | Walk the entire way (no transit, no bicycle) |
| 8 | Bicycle the entire way (no transit) |
| 9 | Walk to local bus |
| 10 | Walk to light rail or ferry |
| 11 | Walk to express bus |
| 12 | Walk to heavy rail |
| 13 | Walk to commuter rail |
| 14 | Drive to local bus |
| 15 | Drive to light rail or ferry ||
| 16 | Drive to express bus |
| 17 | Drive to heavy rail |
| 18 | Drive to commuter rail |
| 19 | Taxi (added in [Travel Model 1.5](TravelModel1.5)) |
| 20 | TNC (Transportation Network Company, or ride-hailing services) - Single party (added in [Travel Model 1.5](TravelModel1.5)) |
| 21 | TNC - Shared e.g. sharing with strangers (added in [Travel Model 1.5](TravelModel1.5)) |