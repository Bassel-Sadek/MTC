[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[PopSynHousehold]]

***

## Household file from Population Synthesizer

The population synthesizer generates this household file and a [person file](PopSynPerson). Variables below in UPPER CASE are drawn directly from PUMS records; variables in lower case are derived from PUMS variables.
 

| *Name* | *Definition* | *Scale* | *Join with &hellip;* |
|--------|--------------|---------|----------------------|
| HHID | Unique household ID number | Integer, any value | All model files |
| TAZ | Transportation analysis zone of home location | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| SERIALNO | PUMA serial number | Long integer, any value |   |
| PUMA5 | PUMA geography from which the drawn household is from (not the PUMA where the household is placed) | Four-digit integer |   |
| HINC | Household income | Year 2000 dollars |   |
| PERSONS | Number of persons in the household | Integer, 1 and up |   |
| HHT | Household/family type | Integer, 1 - family household: married-couple; 2 - family household: male householder, no wife present; 3 - family household: female householder, no husband present; 4 - non-family household: male householder living alone; 5 - non-family household: male householder, not living alone; 6 - non-family household female householder, living alone; 7 - non-family household: female householder, not living alone |   |
| UNITTYPE | Housing unit type | Integer, 0 - housing unit; 1 - institutional group quarters; 2 - non-institutional group quarters |   |
| NOC | Number of own children under 18 years in household | Integer, 0 and up |   |
| BLDGSZ | Building size | Integer, 1 - mobile home; 2 - one-family house detached from any other house; 3 - one-family house attached to one or more houses; 4 - a building with 2 apartments; 5 - a building with 3 or 4 apartments; 6 - a building with 5 to 0 apartments; 7 - a building with 10 to 19 apartments; 8 - a building with 20 to 49 apartments; 9 - a building with 50 or more apartments; 10 - a boat, RV, van, etc. |   |
| TENURE | Home ownership | Integer, 1 - owned by your or someone in this household with a mortgage or loan; 2 - owned by your or someone in this household free and clear; 3 - rented for cash rent; 4 - occupied without payment of cash rent |   |
| VEHICL | Number of vehicles available | Integer, 1 - one vehicle; 2 - two vehicles; 3 - three vehicles; 4 - four vehicles; 5 - five vehicles; 6 - six or more vehicles |   |
| hinccat1 | Household income categorization number 1 | Integer, 1 - 0 to 20k(-); 2 - 20 to 50k; 3 - 50 to 100k; 4 - more than 100k |   |
| hinccat2 | Household income categorization number 2 | Integer, 1 - 0 to 10k; 2 - 10 to 20k; 3 - 20 to 30k; 4 - 30 to 40k; 5 - 40 to 50k; 6 - 50 to 60k; 7 - 60 to 75k; 8 - 75 to 100k; 9 - more than 100k |   |
| hhagecat | Head of household age category | Integer, 1 - 0 to 64 years; 2 - 65 and older |   |
| hsizecat | Household size category | Integer, 1 - one, 2 - two, 3 - three, 4 - four or more |   |
| hfamily | Household family type (HHT-based) | Integer, 1 - non-family household; 2 - family household |   |
| hunittype | Household unit type | Integer, 0 - housing unit; 1 - institutional group quarters; 2 - non-institutional group quarters |   |
| hNOCcat | Number of children category | Integer, 0 - zero; 1 - one or more own chidlren |   |
| hwrkrcat | Number of workers in the household category | Integer, 0 - zero; 1 - one; 2 - two; 3 - three or more |   |
| h0004 | Household members age 0 to 4 | Integer, 0 and up |   |
| h0511 | Household members age 5 to 11 | Integer, 0 and up |   |
| h1215 | Household members age 12 to 15 | Integer, 0 and up |   |
| h1617 | Household members age 16 to 17 | Integer, 0 and up |   |
| h1824 | Household members age 18 to 24 | Integer, 0 and up |   |
| h2534 | Household members age 25 to 34 | Integer, 0 and up |   |
| h3549 | Household members age 35 to 49 | Integer, 0 and up |   |
| h5064 | Household members age 50 to 64 | Integer, 0 and up |   |
| h6579 | Household members age 65 to 79 | Integer, 0 and up |   |
| h80up | Household members age 80 and older | Integer, 0 and up |   |
| hworkers | Household members who work | Integer, 0 and up |   |
| hwork_f | Household members who work full-time | Integer, 0 to hworkers |   |
| hwork_p | Household members who work part-time | Integer, 0 to hworkers |   |
| huniv | Household members who are university students | Integer, 0 and up |   |
| hnwork | Household members who do not work, do not attend school, and are not retired | Integer, 0 and up |   |
| hretire | Household members who are retired | Integer, 0 and up |   |
| hpresch | Pre-school age children in the household | Integer, 0 and up |   |
| hschpred | School age, pre-driving-age children in the household | Integer, 0 and up |   |
| hschdriv | School age, driving age children in the household | Integer, 0 and up |   |
| htypdwel | Type of dwelling (BLDGSZ based) | Integer, 1 - one-family house detached from any other house; 2 - duplex or apartment; 3 - mobile home, boat, RV, van, etc. |   |
| hownrent | Home ownership | Integer, 1 - own; 2 - rent |   |
| hadnwst | Non-working students in the household | Integer, 0 and up |   |
| hadwpst | Working students in the household | Integer, 0 and up |   |
| hadkids | Adult children living in the household (families with persons age 18 to 24 living in a household with older family members) | Integer, 0 and up |   |
| bucketBin | Used by the population synthesizer | &lt;Internal to software use&gt; |   |
| originalPUMA | PUMA geography from which the drawn household is from (not the PUMA where the hosuehold is placed) | Four-digit integer |   |
| hmultiunit | Multi-unit housing dummy variable | Integer, 0 - single family home; 1 - apartment/mobile home/boat/etc |   |


-- Main.DavidOry - 07 Jun 2011