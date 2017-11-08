[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[PropertiesFile]]

# CT-RAMP Properties File

The CT-RAMP software that executes the demand model portion of the MTC travel model is controlled by a standard Java control or properties file (please see the SystemDesign page for an overview of the model components). Most of the properties in the file are used to facilitate software execution when calibrating the travel model and/or to locate and fix software bugs. Lines in the properties file that begin with a pound (#) sign are comments and are ignored by the Java software.

The table below idenfities, describes, and provides an example for each of the variables expected to be in the properties file by the CT-RAMP software. The properties are listed in groups and ordered based on how likely their values are to be changed between scenario analyses.

## Scenario Setup

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| Project.Directory | String | M:/Projects/2000_03_XXX | File locations specified in the properties file as well as the UtilityExpressionCalculator DataSheet pages are expressed as relative to this file location (note that Java expects forward ("/") rather than back ("\") slashes |
| PopulationSynthesizer. InputToCTRAMP. HouseholdFile | String | /popsyn/HhFile.p2009.2005.csv | File location and name of the [[Household]] file, which is one of the standard InputFiles| 
| PopulationSynthesizer. InputToCTRAMP. PersonFile | String | /popsyn/PersonFile.p2009.2005.csv | File location and name of the [[Person]] file,which is one of the standard InputFiles |
| Model.Random.Seed | Integer | 0 | Random number seed used in the simulation of travel choices; successive runs can vary the seed to measure stochastic variation

 
## Key Inputs

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| TazData.File | String | /landuse/TazData.csv | Location and name of file containing TAZ-level zone data |
| TazWalkShares.File | String | /landuse/WalkAccessBuffers.float.csv | Location and name of file defining the zonal walk shares that fall in the short-walk-to-transit and long-walk-to-transit categories |
| ZonalAccessibilities.file | String | /skims/accessibility.csv | Location and name of file containing zonal accessibility values |
 
## Machine Setup

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| RunModel. MatrixServerAddress | String (IP Address) | 192.168.1.200 | The IP address of the computer serving as the Matrix Manager host (see [[SetupConfiguration]]). Set to "none" if matrix IO operations are to be handled in the main process. If unspecified, default address of "localhost" is used. |
| RunModel. MatrixServerPort | Integer | 1171 | The port through which the node computers communicate with the Matrix Manager host |
| RunModel. HouseholdServerAddress | String (IP Address) | 192.168.1.200 | The IP address of the computer serving as the Household Manager host (see [[SetupConfiguration]]) | 
| RunModel. HouseholdServerPort | Integer | 1132 | The port through which the node computers communicate with the Household Manager host |

## Model Switches

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| RunModel. RereadMatrixDataOnRestart | Boolean | true | If true, a new iteration through the demand model will trigger new skim tables to be read; if false, the skim tables stored in memory will be reused (this is used in calibration). |
| RunModel. RestartWithHhServer | String | none | If set to "none", the synthetic population files are re-read when running a new iteration of the model run. Otherwise, specify to start from a particular model: ao,  imtf, jtf, inmtf, awf, stf. |
| RunModel. UsualWorkAndSchoolLocationChoice | Boolean | true | If true, the usual work and school location model is executed (only set to false during calibration) | 
| UsualWorkAndSchoolLocationChoice. RunFlag.Work | Boolean | true | If true, the usual work location models are executed as part of the usual work and school location sub-model execution (only set to false during calibration) |
| UsualWorkAndSchoolLocationChoice. RunFlag.University | Boolean | true | If true, the usual university location models are executed as part of the usual work and school location sub-model execution (only set to false during calibration) |
| UsualWorkAndSchoolLocationChoice. RunFlag.School | Boolean | true | If true, the usual school location models are executed as part of the usual work and school location sub-model execution (only set to false during calibration) | 
| RunModel. AutoOwnership | Boolean | true | If true, the automobile ownership model is executed (only set to false during calibration) |
| RunModel. FreeParking | Boolean | true | If true, the free parking eligibility model is executed (only set to false during calibration) |
| RunModel. CoordinatedDailyActivityPattern | Boolean | true | If true, the coordinated daily activity pattern model is executed (only set to false during calibration) |
| RunModel. IndividualManatoryTourFrequency | Boolean | true | If true, the individual mandatory tour frequency model is executed (only set to false during calibration) |
| RunModel. MandatoryTourDepartureTimeAndDuration | Boolean | true | If true, the mandatory tour departure time and duration model is executed (only set to false during calibration) |
| RunModel. MandatoryTourModeChoice | Boolean | true | If true, the mandatory tour mode choice model is executed (only set to false during calibration) |
| RunModel. JointTourFrequency | Boolean | true | If true, the joint tour frequency model is executed (only set to false during calibration) |
| RunModel. JointTourLocationChoice | Boolean | true | If true, the joint tour location choice model is executed (only set to false during calibration) |
| RunModel. JointTourDepartureTimeAndDuration | Boolean | true | If true, the joint tour depature time and duration model is executed (only set to false during calibration) |
| RunModel. JointTourModeChoice | Boolean | true | If true, the joint tour mode choice model is executed (only set to false during calibration) |
| RunModel. IndividualNonMandatoryTourFrequency | Boolean | true | If true, the individual non-mandatory tour frequency model is executed (only set to false during calibration) |
| RunModel. IndividualNonManatoryTourLocationChoice | Boolean | true | If true, the individual non-mandatory tour location choice model is executed (only set to false during calibration) |
| RunModel. IndividualNonMandatoryTourDepartureTimeAndDuration | Boolean | true | If true, the individual non-mandatory tour depature time and duration model is executed (only set to false during calibration) |
| RunModel. IndividualNonMandatoryTourModeChoice | Boolean | true | If true, the individual non-mandatory tour mode choice model is executed (only set to false during calibration) |
| RunModel. AtWorkSubTourFrequency | Boolean | true | If true, the at work sub-tour frequency model is executed (only set to false during calibration) |
| RunModel. AtWorkSubTourLocationChoice | Boolean | true | If true, the at work sub-tour location choice model is executed (only set to false during calibration) |
| RunModel. AtWorkSubTourDepartureTimeAndDuration | Boolean | true | If true, the at work sub-tour departure time and duration choice model is executed (only set to false during calibration) |
| RunModel. AtWorkSubTourModeChoice | Boolean | true | If true, the at work sub-tour mode choice model is executed (only set to false during calibration) |
| RunModel. StopFrequency | Boolean | true | If true, the stop frequency model is executed (only set to false during calibration) |
| RunModel. StopLocation | Boolean | true | If true, the stop location model is executed (only set to false during calibration) |


## Model Parameters

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| UsualWorkAndSchoolLocationChoice. SampleOfAlternatives. SampleSize | Integer | 30 | The usual work and school location choice models first apply a simple model to collect a sample of destinations to be evaluated by a more complex model. The number of samples collected via the simple model are defined here. |
| JointTourLocationChoice. SampleOfAlternatives. SampleSize | Integer | 30 | The joint tour location choice models first apply a simple model to collect a sample of destinations to be evaluated by a more complex model. The number of samples collected via the simple model are defined here. |
| IndividualNonMandatoryTourLocationChoice. SampleOfAlternatives. SampleSize | Integer | 30 | The individual non-mandatory tour location choice models first apply a simple model to collect a sample of destinations to be evaluated by a more complex model. The number of samples collected via the simple model are defined here. |
| AtWorkSubtourLocationChoice. SampleOfAlternatives. SampleSize | Integer | 30 | The at work sub-tour location choice models first apply a simple model to collect a sample of destinations to be evaluated by a more complex model. The number of samples collected via the simple model are defined here. |
| StopLocationSoa. SampleSize | Integer | 30 | The stop location choice models first apply a simple model to collect a sample of destinations to be evaluated by a more complex model. The number of samples collected via the simple model are defined here. |
| UsualWorkAndSchoolLocationChoice. ShadowPricingFlag. GradeSchool | Boolean | false | If true, shadow pricing is not applied to grade-school location choice. |
| HouseholdManager. MinValueOfTime | Float | 1.0 | A value of time is drawn from one of four distributions (based on household income) for each simulated traveler; this field defines the minimum value of time assigned to a traveler (unit: year 2000 dollars per hour) |
| HouseholdManager. MaxValueOfTime | Float | 50.0 | A value of time is drawn from one of four distributions (based on household income) for each simulated traveler; this field defines the maximum value of time assigned to a traveler (unit: year 2000 dollars per hour) |
| HouseholdManager. LowInc. MeanValueOfTime | Float | 6.01 | A value of time is drawn from one of four distributions (based on household income) for each simulated traveler; this field defines the mean value for the lowest income quartile (unit: year 2000 dollars per hour) |
| HouseholdManager. MidInc. MeanValueOfTime | Float | 8.81 | A value of time is drawn from one of four distributions (based on household income) for each simulated traveler; this field defines the mean value for the second lowest income quartile (unit: year 2000 dollars per hour) |
| HouseholdManager. HighInc. MeanValueOfTime | Float | 10.44 | A value of time is drawn from one of four distributions (based on household income) for each simulated traveler; this field defines the mean value for the second highest income quartile (unit: year 2000 dollars per hour) |
| HouseholdManager. VeryHighInc. MeanValueOfTime | Float | 12.86 | A value of time is drawn from one of four distributions (based on household income) for each simulated traveler; this field defines the mean value for the highest income quartile (unit: year 2000 dollars per hour)|


## Model-Specific Inputs

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| UecFile.  DestinationChoice | String | CTRAMP/model/ DestinationChoice.xls | File location and name of the UtilityExpressionCalculator for the location choice models |
| UecFile. SampleOfAlternativesChoice | String | CTRAMP/model/ DestinationChoiceAlternativeSample.xls | File location and name of the UtilityExpressionCalculator for the location choice alternative sampling models |
| UecFile. AutoOwnership | String | CTRAMP/model/ AutoOwnership.xls | File location and name of the UtilityExpressionCalculator for the automobile ownership model |
| UecFile. FreeParking | String | CTRAMP/model/ FreeParkingEligibility.xls | File location and name of the UtilityExpressionCalculator for the free parking eligibility model |
| UecFile. CoordinatedDailyActivityPattern | String | CTRAMP/model/ CoordinatedDailyActivityPattern.xls | File location and name of the UtilityExpressionCalculator for the coordinated daily activity pattern model |
| UecFile. TourModeChoice | String | CTRAMP/model/ ModeChoice.xls | File location and name of the UtilityExpressionCalculator for the tour mode choice model |
| UecFile. IndividualMandatoryTourFrequency | String | CTRAMP/model/ IndividualMandatoryTourFrequency.xls | File location and name of the UtilityExpressionCalculator for the individual mandatory tour frequency model |
| UecFile. TourDepartureTimeAndDuration | String | CTRAMP/model/ TourDepatureAndDuration.xls | File location and name of the UtilityExpressionCalculator for the tour departure and duration time models |
| UecFile. AtWorkSubtourFrequency | String | CTRAMP/model/ AtWorkSubtourFrequency.xls | File location and name of the UtilityExpressionCalculator for the at work sub-tour frequency models |
| UecFile. JointTourFrequency | String | CTRAMP/model/ JointTours.xls | File location and name of the UtilityExpressionCalculator for the joint tour generation models |
| UecFile. IndividualNonMandatoryTourFrequency | String | CTRAMP/model/ IndividualNonMandatory TourFrequency.xls | File location and name of the UtilityExpressionCalculator for the individual non-mandatory tour frequency models |
| UecFile. StopFrequency | String | CTRAMP/model/ StopFrequency.xls | File location and name of the UtilityExpressionCalculator for the stop frequency models |
| UecFile. StopLocation | String | CTRAMP/model/ StopDestinationChoice.xls | File location and name of the UtilityExpressionCalculator for the stop location choice models |
| UecFile. StopLocationSoa | String | CTRAMP/model/ StopDestinationChoiceAlternativeSample.xls | File location and name of the UtilityExpressionCalculator for the stop location choice sample of alternatives |
| UecFile. TripModeChoice | String | CTRAMP/model/ TripModeChoice.xls | File location and name of the UtilityExpressionCalculator for the trip mode choice models |
| UecFile. ParkingLocationChoice | String | CTRAMP/model/ ParkingLocationChoice.xls | File location and name of the UtilityExpressionCalculator for the parking location choice models |
| UsualWorkAndSchoolLocationChoice. SizeCoefficients. InputFile | String | CTRAMP/model/ DestinationChoiceSizeCoefficients.csv | File location and name of the size term (i.e. attraction) model coefficients for the tour destination choice models |
| UsualWorkAndSchoolLocationChoice. AlternativesList. InputFile | String | CTRAMP/model/ DestinationChoiceAlternatives.csv | File location and name of the alternatives available to the destination choice models (part of the model design; this should not be changed) |
| UsualWorkAndSchoolLocationChoice. ShadowPricing. Input.File | String | CTRAMP/model/ ShadowPricing.csv | File location and name of the usual work location shadow price file. The usual work model iteratively assigns workers to locations with enough jobs to satisfy worker demand with shadow prices. The input file is updated during model execution as described on the RunModelBatch page. |
| MandatoryTourDepartureAndDuration. AlterantivesList. InputFile | String | CTRAMP/model/ TourDepartureAndDurationAlternatives.csv | Location and name of a file that defines the alternatives available to the departure time and duration models (see !UecFile.TourDepartureTimeAndDuration) |
| IndividualNonMandatoryTourFrequency. AlternativesList. InputFile | String | CTRAMP/model/ IndividualNonMandatory TourFrequencyAlterantives.csv | Location and name of a file that defines the alternatives available to the individual non-mandatory tour frequency model (see UecFile.IndividualNonMandatory TourFrequency) |
| CBDParkingAlternatives. file | String | CTRAMP/model/ CBDParkingZones.csv | File location and name of the alternative TAZs for parking for the Parking Location Choice model |
| IndividualNonMandatoryTour. FrequencyExtension. ProbabilityFile | String | CTRAMP/model/ IndividualNonMandatory TourFrequencyExtensionProbabilities.csv | Location and name of a file that additionally defines the alternatives in the INMTF model. This additions file is by person_type and tour type and contains the probability of the number of nonmandatory tours by type if an alternative of one or more tours is selected in the INMTF model (see IndividualNonMandatory TourFrequencyAlternatives.csv) |
| StopDestinationChoice. SizeCoefficients. InputFile | String | CTRAMP/model/ StopDestinationChoiceSizeCoefficients.csv | File location and name of the size term (i.e. attraction) model coefficients for the stop location choice models |
| StopPurposeLookup. Proportions | String | CTRAMP/model/ StopPurposeLookup.csv | File location and name of the file that defines the probabilities (i.e. it's simple share model), by primary tour purpose, inbound/outbound leg, departure time, and person type, of making a stop of a given purpose (given a stop is going to be made). |
| TripDepartTime.Proportions | String | CTRAMP/model/ BATS2000_TripHour_ByTourHour_adjusted.csv | File location and name of the file that defines the probabilities (i.e. it's a simple share model), by tour departure time, of trip departure times |


## Output Options

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| Results. WriteDataToFiles | Boolean | true | When calibrating and/or testing only the CT-RAMP portion of the model, writing the output files to disk is unnecessary; the option is made available here |
| Results. HouseholdDataFile | String | main/HouseholdData.csv | File location and name of the [[Household]] output file |
| Results. PersonDataFile | String | main/PersonData.csv | File location and name of the [[Person]] output file |
| Results. IndivTourDataFile | String | main/IndivTourData.csv | File location and name of the IndividualTour output file |
| Results. JointTourDataFile | String | main/JointTourData.csv | File location and name of the JointTour output file |
| Results. IndivTripDataFile | String | main/IndivTripData.csv | File location and name of the IndividualTrip output file |
| Results. JointTripDataFile | String | main/JointTripData.csv | File location and name of the JointTrip output file |
| Results. UsualWorkAndSchoolLocationChoice | String | main/wsLocResults.csv | File location and name of the MandatoryLocation output file |
| Results. AutoOwnership | String | main/aoResults.csv | Location and name of the file that includes results from the automobile ownership model (these results are also in the [[Household]] file) (file used primarily for calibration) |
| Results. CoordinatedDailyActivityPattern | String | main/cdapResults.csv | Location and name of the file that includes results specific to the coordinated daily activity pattern model (these results are also in the [[Person]] file) (file used primarily for calibration) |
| Results. IndividualMandatoryTourFrequency | String | main/imtfResults.csv | Location and name of the file that includes results specific to the individual mandatory tour frequency model (these results are also in the IndividualTour file) (file used primarily for calibration) |
| Results. JointTour | String | main/jointModelsResults | Location and name of the file that includes results specific to all the joint tour models (these results are also in the JointTour file) (file used primarily for calibration) |
| Results. IndividualNonMandatoryTour | String | main/indivNonMandatoryTourResults.csv | Location and name of the file that includes results specific to the individual non-mandatory tour models (these results are also in the IndividualTour file) (file used primarily for calibration) |
| Results. AtWorkSubtour | String | main/atWorkSubtourResults.csv | Location and name of the file that includes results specific to the at work sub-tour models (these results are also in the IndividualTour file) (file used primarily for calibration) |
| Results. TourStop | String | main/tourStopResults.csv | Location and name of the file that includes results specific to the stop models (these results are also in the IndividualTrip file) (file used primarily for calibration) |
| UsualWorkAndSchoolLocationChoice. ShadowPricing. OutputFile | String | CTRAMP/model/ ShadowPricing.csv | File location and name of the output usual work location shadow price file. This file can be read as the ShadowPricing.Input.File. |

 
## Computational Parameters

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| distributed. task.packet.size | Integer | 5000 | Number of households in each JPPF worker task sent to a remote worker node |
| initialization. packet.size | Integer | 500 | Initial number of households to send to worker nodes |
| number. initialization. packets | Integer | 20 | Number of initial packets to create when initializing the worker nodes |

## Debug Options

| Property | Data Type | Example Value | Description |
|----------|-----------|---------------|-------------|
| Debug.Trace.HouseholdIdList | Integers | 2047857,2231509 | Detailed output used to facilitate debugging is generated for simulated households with the household ID numbers listed here |
| Run.This.Household.Only | Integer | 1357122 | The travel model simulates only the household with the household ID specified here |

-- Main.BenStabler - 12 Feb 2012