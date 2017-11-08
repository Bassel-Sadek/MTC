[[Home]] > [[TravelModel]] > [[Development]] > [[TravelModelOneV06]]

---

# What is Travel Model One (v 0.6)?

Travel Model One v0.6 differes from [Travel Model One v0.5](TravelModelOneV05) in that it adds trips to and from Bay Area High Speed Rail (HSR) stations based on output from the California HSR Business Plan Model-Version 3.

# Inputs
* California HSR trip tables relevant for the Bay Area HSR stations are now required, for the HSR model years (2025, 2029, and 2040).

# Process
* Preprocessing: Create HSR trip tables to/from Bay Area stations based on Model Year and HSR model output
  * Non Resident Model:
  * Choose transit submode for transit trips to/from Bay Area HSR stations.
  * Choose toll/no toll for drive trips to/from Bay Area HSR stations and add these trips to auto trip tables
* Prepassign: Add transit trips to/from Bay Area HSR stations to the transit trip tables