[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[WalkAccessBuffers]]

***

To ameliorate the impact of MTC's large travel analysis zones (TAZ) on travel-related decisions, each TAZ is segmented into one of three non-spatial sub-zones, as follows: (i) the percent of activities located within a short-walk to transit (defined as one-third of a mile); (ii) percent of activities located within a long-walk to transit (defined as two-thirds of a mile); and, (iii) percent of activities that cannot be accessed on foot from transit. When making location decisions, simulated travelers select a TAZ as well as a sub-zone. The sub-zones are defined by a CSV file with the following column headers and data values:
* *TAZ* - The travel analysis zone number (Integer);
* *SHRT* - The probability of an activity in this zone occuring within a short-walk to transit (Float);
* *LONG* - The probability of an activity in this zone occurring between a short- and long-walk to transit (Float).

-- Main.DavidOry - 27 Jan 2012