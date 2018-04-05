[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[MandatoryLocation]]

----
Simulation results specific to mandatory location decisions.

| Name | Definition | Scale | Join with  |
|---|---|---|---|
| HHID | Unique household ID number | Long integer, any value | All model files,[synthetic population household file](PopSynHousehold) |
| HomeTAZ | Home transportation analysis zone | Integer, 1 to 1454 | [Shape file](https://mtc.maps.arcgis.com/home/item.html?id=b85ba4d43f9843128d3542260d9a2f1f) |
| HomeSubZone | Walk to transit home sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit | |
| Income | Annual household income ($2000) | Integer, 0 and up | |
| PersonID | Unique person ID number | Long integer, any value | [Synthetic population person file](PopSynPerson), [[Person]] |
| PersonNum | Person number unique to the household | Integer, 1 to household size | |
| PersonType | Person lifestage/employment type | Integer, 1 - Full-time worker; 2 - Part-time worker; 3 - University student; 4 - Nonworker; 5 - Retired; 6 - Student of non-driving age; 7 - Student of driving age; 8 - Child too young for school | |
| PersonAge | Person age | Integer, 0 and up | |
| EmploymentCategory | Employment category | String, "Full-time worker", "Part-time worker", "Not employed" | |
| StudentCategory | Student category | String, "College or higher", "Grade or high school", "Not student" | |
| WorkLocation | Work location transportation analysis zone | Integer, 1 to 1454, or 0 if no workplace is selected | |
| WorkSubZone | Walk to transit work sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit | |
| SchoolLocation | School location transportation analysis zone | Integer, 1 to 1454, or 0 if no workplace is selected | |
| SchoolSubZone | Walk to transit school sub-zone (not located in space) | Integer, 0 - cannot walk to transit; 1 - short-walk to transit; 2 - long-walk to transit | |
 

-- Main.DavidOry - 07 Jun 2011