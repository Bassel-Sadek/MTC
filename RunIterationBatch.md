[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[RunModel]] > [[RunModelBatch]] > [[RunIterationBatch]]

***

# Run Iteration Batch File: Details

The *RunIteration.bat* file is called repeatedly by the RunModelBatch file during execution of the MTC travel model. This page explicates the steps incuded in the *RunIteration.bat* instructions. Please note that if RunModelBatch is on iteration 0, the first three steps in the process described below are skipped.

## Step 1: Build highway and transit skims

Five separate Cube scripts are responsible for creating the highway and transit level-of-service matrices (commonly referred to as "skims") that serve as the network description for the CT-RAMP choice models. These scripts are as follows:

1. **HwySkims.job** -- Uses the congested network to build level-of-service matrices segmented by time-of-day (see the TimePeriods page), vehicle occupancy class, vehicle value-toll-paying willingness (i.e. willingness to pay a high-occupancy toll lane fee), and vehicle use type (personal or commercial).
1. <strong>PrepHwyNet.job </strong>-- This script prepares the highway network for use by the transit network. Specifically, it uses a simple model (a fixed delay per mile segmented by area type) to compute a bus travel time estimate on every roadway link. Second, it adds transit-only access links.
1. <strong>BuildTransitNetworks.job </strong>-- Here, the following transit support links are created: (a) walk access links from zone centroids to bus stops (located on the highway network) and zone centroids to walk access funnel links for transit-only infrastructure; (b) drive access links are generated from zone centroids to park-and-ride facilities; (c) GAWK is used to use the access links to create egress links (transposing the A and B nodes); (d) transit transfer links are created and combined with the access and egress links; and, (e) GAWK is used to select the two best park-and-ride lots for each zone for each type of line haul facility that has park and ride lots.
1. **TransitSkims.job** -- Transit level-of-service matrices are created from the transit networks. These skims are segmented by TimePeriods, access mode (walk or drive), egress mode (walk or drive), and path.
1. <strong>Accessibility.job </strong>-- The Automobile Ownership model uses various measures of accessibility to assess the difficulty travelying by automobile, transit, or non-motorized (bicycle, walk) modes from each travel analysis zone.
Each of the above scripts has more detailed descriptions of the processess embedded as comments in the script file.

## Step 2: Execute the choice models using CT-RAMP Java code

The !MtcTourBasedModel Java class executes the choice model categories numbered 2 through 5 in the ModelSchematic. A single command line call to Java is used to execute the software; the following parameters, many of which are set in the [[SetupConfiguration]] page, are used in the call:



|  Parameter  |  Purpose  |
|-------------|-----------|
| showversion | Displays the Java version information |
| Xmx6000m | Allow the Java virtual machine no more than 6 GB of RAM |
| cp %CLASSPATH% | Set the Java classpath to the CLASSPATH environment variable (see RunModelBatch) |
| log4j.configuration = log4j.xml | The <a href="http://en.wikipedia.org/wiki/Log4j" target="_blank" title="Wikipedia log4j page">log4j</a> class logs output per the log4j.xml file |
| JAVA_HOME_32= "%JAVA_PATH_32%" | The 32-bit Java virtual machine, required to communicate with the Matrix Manager, is located here |
| JAVA_32_PORT = 1181 | The Port through which communication is done to the Matrix Manager |
| java.library.path = %RUNTIME% | The MTC.JAR file contains numerous Java classes used by the software |
| jppf.config = jppf-client properties | The JPPF configuration file |
| iteration %ITER% | Iteration of the model for identifying outputs |
| sampleRate %SAMPLESHARE% | The share of the synthetic population whose behavior is simulated via the choice models |
| sampleSeed %SEED% | Random number seed |
 
## Step 3: Execute the internal/external and commercial vehicle models

Representations of internal/external travel (i.e. travel that either starts or ends outside the nine county Bay Area) and commercial vehicle travel are generated outside the CT-RAMP software. The following scripts implement these models:

1. **IxTimeOfDay.job** -- The internal/external model begins with fixed daily trip tables in production/attraction format; these tables are based on census commute flows and represent single-, double-, and three-or-more occupant private vehicles. In this script, the daily trip tables are segmented into time-of-day specific origin-destination matrices using diurnal factors developed for MTC's BAYCAST trip-based model.
1. <strong>IxTollChoice.job </strong>-- Internal/external travelers are presented the option of paying a fee to use a high-occupancy toll. Here, a simple binary logit model is used to segment internal/external travelers by occupancy category into those willing to a pay a toll and those not willing to pay a toll.
1. <strong>TruckTripGeneration.job </strong>-- Commercial vehicle travel is generated here, the first in a simple four step commercial vehicle model. Four truck classes are explicitly considered throughout the commercial vehicle model as follows: very small trucks (two-axle, four-tire), small trucks (two-axle, six tire), medium trucks (three-axle), and large or combination trucks (four or more axles).
1. **TruckTripDistribution.job** -- Commercial vehicles are distributed using a gravity model. The gravity model uses travel time as the measure of impedance.
1. <strong>TruckTimeOfDay.job </strong>-- Fixed diurnal factors are used to translate the production/attraction matrices from the distribution model to time-of-day-specific origin/destination matrices.
1. <strong>TruckTollChoice </strong>-- Similar to the *IxTollChoice.job* script, this script implements a simple binary logit model to segment trucks, by vehicle class, into those willing to pay a toll and those not willing to pay a toll.
Please see the actual script files for more complete details about these processes. 

## Step 4: Build matrices from trip lists and assign trips to the highway network

The travel model simulates the individual behavior of each resident in the nine county Bay Area. Two outcomes of this simulation are (i) a list of trips made by individuals, fully identified by time of day, travel mode, and origin/destination; and, (ii) a list of trips made by two or more members of the same household (so-called "joint" travel). The *PrepAssign.job* file takes these trip lists and converts them to origin/destination trip matrices; trip matrices can be assigned to the highway network using the standard user equilibrium procedures. When translating these lists to matrices, the SAMPLESHARE environment variable is used to scale the trips such that the simulated sample represents the full population (e.g., if a 50 percent sample is simulated, then each trip made by a simulated traveler represents two trips in the trip matrices).

The highway assignment step (*HwyAssign.job*) combines the internal/external, commercial vehicle, and resident travel matrices and loads them to the highway network. A total of ten vehicle classes are maintained during assignment, as follows:

1. Drive alone (single-occupant passenger vehicles), <em>not </em>willing to pay a toll to use a high-occupancy toll (HOT) lane ("not-value-toll-eligible);
1. Shared ride 2 (double-occupant passenger vehicles), _not_ willing to pay a toll to use an HOT lane;
1. Shared ride 3+ (three-or-more-occupant passenger vehicles), _not_ willing to pay a toll to use an HOT lane;
1. Very small, small, and medium trucks, <em>not </em>willing to pay a toll to use an HOT lane;
1. Large/combination trucks, <em>not </em>willing to pay a toll to use an HOT lane;
1. Drive alone, willing to pay a toll to use an HOT lane;
1. Shared ride 2, willing to pay a toll to use an HOT lane;
1. Shared ride 3+, willing to pay a toll to use an HOT lane;
1. Very small, small, and medium trucks, willing to pay a toll to use an HOT lane; and,
1. Large/combination trucks, willing to pay a toll to use an HOT lane.

The highway assignment results in estimates of congested speed; the [[LoadedHighway]] page details the output from this step. Please see the scripts themselves for complete details regarding the conversion of trip lists to trip tables and the highway assignment. The code which implements this step is shown below. Note that the *PrepAssign.job* routine is only called when the ITER environment variable is greater than 0 (no trip lists existing prior to the first iteration; the 0th iteration of [[RunIterationBatch]] only assigns the warm start trip tables to the highway network, as discussed in [[RunModelBatch]]).

## Step 5: Prepare the networks for the next iteration

After the assignment of vehicles to the roadway is complete, the roadway network is processed in preparation for the next iteration of the demand models. The specific steps in this process are as follows:

1. Create a folder named <strong>iter[X] </strong>(where [X] is the iteration number) in the <strong>hwy </strong>directory in which to store the assignment results;
1. Move the loaded highway networks (five are created, by time of day) into the <strong>hwy\iter[X] </strong>folder;
1. Execute *RenameAssignmentVariables.job*, a script that replaces the Cube default variable names with more intuitive names;
1. Execute *AverageNetworkVolumes.job*, a script that uses the PREV_ITER, ITER, PREV_WGT, and WGT environment variables to compute a weighted average between the roadway volumes from the previous and current iterations;
1. Execute *CalculateSpeeds.job*, a script that uses the volume computed in the previous step and the MTC volume-delay functions to compute the expected speed for the computed volume;
1. Execute *TestNetworkConvergence.job*, a script that compares roadway network statistics between the previous and current iterations of the roadway network; and,
1. Execute *MergeNetworks.job*, a script that combines the time-of-day-specific networks into a single network,computes daily network characteristics, and writes out a CSV version of the daily network file.
Once complete, these steps create a network with a representation of congested speeds that are fed into the next iteration of the demand models. The user of the model is required to examine the output from the *TestNetworkConvergence.job* script to determine if the network has stablized to a sufficient degree to determine that additional iterations of the demand model and not necessary.

-- Main.DavidOry - 20 Jan 2012