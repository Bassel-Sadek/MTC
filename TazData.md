[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[TazData]]

***

Identical CSV and DBF versions of this file are used by the travel model.

| *Name* | *Definition* | *Scale* | *Join with &hellip;* |
|--------|--------------|---------|----------------------|
| ZONE | Transportation analysis zone | Integer, 1 to 1454 | Origins, destinations, [shape file](http://opendata.mtc.ca.gov/datasets/b85ba4d43f9843128d3542260d9a2f1f_0) |
| DISTRICT | Superdistrict geographic designation | Integer, 1 to 34 |   |
| SD | Superdistrict geographic designation (duplicate) | Integer, 1 to 34 |   |
| COUNTY | County | Integer, 1 to 9 | 1=San Francisco; 2=San Mateo; 3=Santa Clara; 4=Alameda; 5=Contra Costa; 6=Solano; 7= Napa; 8=Sonoma; 9=Marin |
| TOTHH | Total households | Integer, 0 and up |   |
| HHPOP | Population living in households (as opposed to group quarters) | Integer, 0 and up |   |
| TOTPOP | Total population | Integer, 0 and up |   |
| EMPRES | Employed residents | Integer, 0 and up |   |
| SFDU | Number of occupied single-family dwelling units | Integer, 0 and up |   |
| MFDU | Number of occupied multi-family dwelling units | Integer, 0 and up |   |
| HHINCQ1 | Households in the lowest income quartile (less than $30,000 annually in $1999) | Integer, 0 and up |   |
| HHINCQ2 | Households in the second lowest income quartile (between $30,000 and $60,000 in $1999) | Integer, 0 and up |   |
| HHINCQ3 | Households in the second highest income quartile (between $60,000 and $100,000 in $1999) | Integer, 0 and up |   |
| HHINCQ4 | Households in the highest income quartile (more than $100,000 in $1999) | Integer, 0 and up |   |
| TOTACRE | Total acres | Float, 0.0 and up |   |
| RESACRE | Acres occupied by residential development | Integer, 0 and up |   |
| CIACRE | Acres occupied by commercial or industrial development | Integer, 0 and up |   |
| !SHPOP62P | Share of the population age 62 or older | Float, 0.0 to 1.00 |   |
| TOTEMP | Total employment | Integer, 0 and up |   |
| AGE0004 | Persons age 0 to 4 | Integer, 0 and up |   |
| AGE0519 | Persons age 5 to 19 | Integer, 0 and up |   |
| AGE2044 | Persons age 20 to 44 | Integer, 0 and up |   |
| AGE4564 | Persons age 45 to 64 | Integer, 0 and up |   |
| !AGE65P | Persons age 65 and older | Integer, 0 and up |   |
| RETEMPN | Retail trade employment ([NAICS-based](http://www.census.gov/eos/www/naics/)) | Integer, 0 and up |   |
| FPSEMPN | Financial and professional services employment (NAICS-based) | Integer, 0 and up |   |
| HEREEMPN | Health, educational and recreational service employment (NAICS-based) | Integer, 0 and up |   |
| AGREMPN | Agricultural and natural resources employment (NAICS-based) | Integer, 0 and up |   |
| MWTEMPN | Manufacturing, wholesale trade and transportation employment (NAICS-based) | Integer, 0 and up |   |
| OTHEMPN | Other employment (NAICS-based) | Integer, 0 and up |   |
| PRKCST | Hourly parking rate paid by long-term (8-hours) parkers (year 2000 cents) | Float, 0.0 and up |   |
| OPRKCST | Hourly parking rate paid by short-term parkers (year 2000 cents) | Float, 0.0 and up |   |
| AREATYPE | Area type designation | Integer, 0=regional core, 1=central business district, 2=urban business, 3=urban, 4=suburban, 5=rural |   |
| HSENROLL | High school students enrolled at schools in this TAZ | Float, 0.0 and up |   |
| COLLFTE | College students enrolled full-time at colleges in this TAZ | Float, 0.0 and up |   |
| COLLPTE | College students enrolled part-time at colleges in this TAZ | Float, 0.0 and up |   |
| TERMINAL | Average time to travel from automobile storage location to origin/destination | Float, 0.0 and up |   |
| TOPOLOGY | Topology (steepness) indicator | Integer, 1 - flat, 2 - in between, 3 - steep |   |
| ZERO | Placeholder (always zero) | Integer, 0 |   |
| HHLDS | Repeat of the TOTHH variable with a different name for software compatibility | Integer, 0 and up |   |
| SFTAZ | Repeat of the ZONE variable with a different name for software compatibility | Integer, 1 to 1454 |   |
| GQPOP | Population living in group quarters rather than households | Integer, 0 and up |   |


-- Main.DavidOry - 04 Jan 2013