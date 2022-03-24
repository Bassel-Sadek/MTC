[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]]

***

## Definitions of variables in key input files

* [[TazData]] - Land use (zonal) data
* [[PopSynHousehold]] - Household data file from the population synthesizer
* [[PopSynPerson]] - Person data file from the population synthesizer
* [[TruckDistribution]] - Commercial vehicle model parameters
* [[FixedDemand]] - Internal/external and air passenger travel

## Definitions of variables in key output files

* [[Household]] - Model simulation results specific to households
* [[Person]] - Model simulation results specific to persons
* [[MandatoryLocation]] - Model simulation results specific to mandatory location decisions
* [[IndividualTour]] - Model simulation results specific to individual tours
* [[IndividualTrip]] - Model simulation results specific to individual trips
* [[JointTour]] - Model simulation results specific to joint tours
* [[JointTrip]] - Model simulation results specific to joint trips
* PersonTripTables - Model simulation results presented as resident person travel flows.  Prior to executing the roadway and transit assignment steps of the model (which generate the [[LoadedHighway]] and [[LoadedTransit]] file sets), the [[IndividualTrip]] and [[JointTrip]] lists are consolidated into [[TimePeriods]] and [[TravelModes]] specific trip tables. These tables include the trip flows of residents of the nine county Bay Area made other locations within the nine county Bay Area.
* [[SimpleSkims]] - Simplified level-of-service matrices ("skims")
* [[TransitSkims]] - Detailed outputs from the transit skimming procedure
* [[LoadedHighway]] - Model simulation results specific to roadway usage
* [[LoadedTransit]] - Model simulation results specific to transit routes
* [[ShadowPrice]] - Implementation details of destination choice shadow pricing
* [CoreSummaries](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/scripts/core_summaries/Readme.md) - Core Summaries tables

## Definitions of key parameters

* [[TimePeriods]] - Temporal resolution of the travel model
* [[TravelModes]] - Definitions of means of travel
* [[SpeedCapacity]] - Free flow speed and capacity look up tables

-- Main.DavidOry - 06 Jun 2011