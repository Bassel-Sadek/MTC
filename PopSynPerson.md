[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[PopSynPerson]]

***

## Person file from Population Synthesizer

The population synthesizer generates a [household file](PopSynHousehold) and this person file. Variables below in UPPER CASE are drawn directly from PUMS records; variables in lower case are derived from PUMS variables.

| Name | Definition | Scale | Join with  |
|------|------------|-------|--------------|
| HHID | Unique household ID number | Integer, any value | All model files, [synthetic population household file](PopSynHousehold) |
| PERID | Unique person ID number | Integer, any value | Model files specific to persons and individual travel |
| AGE | Person's age in years | Integer, 0 and up | |
| RELATE | Relationship to householder | Integer, 1 - householder; 2 - husband/wife; 3 - natural born child; 4 - adopted child; 5 - step child; 6 - sibling; 7 - parent; 8 - grandchild; 9 - parent-in-law; 10 - son/daughter-in-law; 11 - other relative; 12 - brother/sister-in-law; 13 - nephew/niece; 14 - grandparent; 15 - uncle/aunt; 16 - cousin; 17 - roomer/boarder; 18 - housemate/roommate; 19 - unmarried partner; 20 - foster child; 21 - other nonrelative; 22 - institutionalized GQ person; 23 - non-institutionalized GQ person | |
| ESR | Employment status | Integer, 0 - under sixteen; 1 - employed, at work; 2 - employed, with a job but not at work; 3 - unemployed; 4 - armed forces, at work; 5 - armed forces, with a job but not at work; 6 - not in labor force | |
| GRADE | Grade of students or children under 3 | Integer, 0 - not a student; 1 - nursery school; 2 - kindergarten; 3 - grade 1 to 4; 4 - grade 5 to 8; 5 - grade 9 to 12; 6 - college undergraduate; 7 - graduate or professional school | |
| PNUM | Person number unique to the household | Integer, 1 and up | |
| PAUG | Augmented (imputed data) person flag | Integer, 0 - not augmented; 1 - augmented | |
| DDP | Data-defined (imputed data) person flag | Integer, 0 - collected; 1 - imputed by edit; 2 - imputed by substitution | |
| SEX | Gender | Integer, 1 - male; 2 - female | |
| WEEKS | Weeks worked in 1999 | Integer, 0 to 52 | |
| HOURS | Hours worked per week in 1999 | Integer, 0 to 99 | |
| MSP | Marital status | Integer, 0 - N/A; 1 - Now married, spouse present; 2 - Now married, spouse absent; 3 - Widowed; 4 - Divorced; 5 - Separated; 6 - Never married | |
| POVERTY | Poverty status | Real, 0 - unrelated children/military; &gt;0 percentage of poverty rate, up to 500 percent | |
| EARNS | Personal income | Integer, up to $325,000 | |
| pagecat | Age category | Integer, 0 - less than five; 1 - five to eleven; 2 - twelve to fifteen; 3 - sixteen and seventeen; 4 - eighteen to twenty-four; 5 - twenty-five to thirty-four; 6 - thirty-five to forty-nine; 7 - fifty to sixty-four; 8 - sixty-five to seventy-nine; 9 - eighty and older | |
| pemploy | Employment status | Integer, 1 - full-time worker; 2 - part-time worker; 3 - not in the labor force; 4 - student under 16 | |
| pstudent | Student status | Integer, 1 - pre-school through grade 12 student; 2 - university/professional school student; 3 - non-student | |
| ptype | Person type | Integer, 1 - full-time worker; 2 - part-time worker; 3 - college student; 4 - non-working adult; 5 - retired; 6 - driving-age student; 7 - non-driving age student; 8 - child too young for school | |
| padkid | Person is adult kid living at home | Integer, 1 - adult child at home; 2 - not adult child at home | |


-- Main.DavidOry - 07 Jun 2011