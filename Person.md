[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[Person]]

---

# Person results from Travel Model

Person-specific results from the travel model simulation.

| Name | Definition | Scale | Join with  |
|---|---|---|---|
| hh_id | Unique household ID number | Long integer, any value | All model files, [synthetic population household file](PopSynHousehold), [[Household]] |
| person_id | Unique person ID number | Long integer, any value | [Synthetic population person file](PopSynPerson) |
| person_num | Person number unique to the household | Integer, 1 to household size | |
| age | Person age | Integer, 0 and up | |
| gender | Person gender | String, "m" - male; "f" - female | |
| type | Person lifestage/employment type | String, "Full-time worker"; "Part-time worker"; "University student"; "Nonworker"; "Retired"; "Student of non-driving age"; "Student of driving age"; "Child too young for school" | |
| value_of_time | Value of time ($2000 per hour).  Calculated [here](https://github.com/BayAreaMetro/travel-model-one/blob/master/core/projects/mtc/src/java/com/pb/mtc/ctramp/MtcHouseholdDataManager.java#L323) with [parameters](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/runtime/mtcTourBased.properties#L131) | Float, 0 and up | |
| fp_choice | Free parking eligibility choice | Integer, 1 - person will park for free; 2 -person will pay to park | |
| activity_pattern | Primary daily activity pattern | String, "M" - mandatory; "N" - non-mandatory; "H" - home | |
| imf_choice | Individual mandatory tour frequency | Integer, 1 - one work tour; 2 - two work tours; 3 - one school tour; 4 - two school tours; 5 - one work tour and one school tour | |
| inmf_choice | Individual non-mandatory tour frequency | Integer, 1 to 96, see IndividualNonMandatoryTourFrequencyAlternatives.csv | |
 

-- Main.DavidOry - 07 Jun 2011