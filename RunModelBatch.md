[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[RunModel]] >> [[RunModelBatch]]

***

# Run Model Batch File: Details

The MTC travel model uses two MS-DOS batch files to proceed through the steps of the travel model. This page discusses the *RunModel.bat* file, which calls, repeatedly, the *RunIteration.bat* file, which is described on the RunIterationBatch page.

## Step 1: Set the necessary path variables

As discussed on the SetupConfiguration page, the travel model requires access to Java, GAWK, and Cube software. The [SetPath.bat](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/runtime/SetPath.bat) script sets up the locations of these paths.

## Step 2: Create directory structure

The second step in the *RunModel.bat* file is to create the directory structure on which the model will operate. The following nine folders are created:
1. <strong>hwy </strong>(highway inputs and outputs)
1. <strong>trn </strong>(transit inputs and outputs)
1. <strong>skims </strong>(level-of-service matrices, or skims, outputs)
1. **landuse** (land use or travel analysis zone-specific inputs)
1. <strong>popsyn </strong>(synthetic population inputs)
1. <strong>nonres </strong>(non-residential inputs and outputs)
1. <strong>main </strong>(choice model result outputs)
1. <strong> logs </strong>(log files, temporary outputs)
1. **database** (simplified skim database outputs)

Next, the data stored in the INPUT folders is copied to this folder structure. Doing this allows the INPUT data to remain untouched during model execution. The actual instructions are below.

```
mkdir hwy
mkdir trn
mkdir skims
mkdir landuse
mkdir popsyn
mkdir nonres
mkdir main
mkdir logs
mkdir database

copy INPUT\hwy\ hwy\
copy INPUT\trn\transit_lines\ trn\
copy INPUT\trn\transit_fares\ trn\
copy INPUT\trn\transit_support\ trn\
copy INPUT\landuse\ landuse\
copy INPUT\popsyn\ popsyn\
copy INPUT\nonres\ nonres\
copy INPUT\warmstart\main\ main\
copy INPUT\warmstart\nonres\ nonres\
```
## Step 3: Pre-process steps

Prior to executing the travel model, three steps are taken to refine the details in the highway network. These steps are accomplished by three Cube scripts as follows:

1. *SetTolls.job* -- The roadway network contains both bridge and so-called value tolls. The former are charged to motorists wishing to cross one of the Bay Area's eight toll bridges; the latter is charged to motorists wishing to travel along a parallel or nearby route, typically on a high-occupancy toll (HOT) lane. The monetary prices are set to specific links, by time of day, by this script. These prices do not change as the model iterations are performed, so need to be set only once in the model flow. The script, which can be edited in a text editor, contains complete details regarding its functions and assumptions.
1. <strong>SetHovXferPenalties.job </strong>-- The manner in which roadways are represented in the travel model does not allow for the explicit representation of lane changing behavior. Most all of the high-occupancy vehicle (HOV) lanes in the Bay Area are situated as the left-most lane on highway segments, making it a bit difficult to navigate from on-ramps and to off-ramps, which are generally connected to the right-most lane on highway segments. In an attempt to capture the perceived difficulty of navigating from the general purpose lanes to an HOV lane, a time penalty of 30 seconds is applied to the dummy links which connect the general purpose lanes and the HOV/HOT lanes in the travel model.
1. <strong>CreateFiveHighwayNetworks.job </strong>-- There are a handful of instances in which the roadway network's configuration differs temporally during a typical weekday. Specifically: (a) the Caldecott tunnel uses changeable lanes to accommodate more traffic in the peak direction; (b) the Golden Gate Bridge uses changeable lanes to accommodate more traffic in the peak direction; (c) HOV lanes turn into general purpose lanes during the off-peak periods; (d) the Sterling on-ramp in downtown San Francisco allows HOVs only in the peak periods; (e) HOV toll bypass lanes on bridges turn into general purpose lanes that must pay the toll; and, (f) the amount of delay at the Bay Area's bridge toll booths, vary (the travel model assumes a fixed amount of delay by time of day). Each of these configurations are defined for each of the TimePeriods used by the travel model in this script. This script also prevents park-and-ride links (meaning connections from origin locations to park-and-ride locations) from being drawn across the Bay Area's toll bridges (with certain exceptions), explicitly assuming that travelers will not cross a toll bridge to utilize a park-and-ride facility.
As noted above, complete details regarding the function, input files, output files, and assumptions made in these scripts are documented in the scripts themselves. The actual instructions for the pre-process steps are presented below. Note that whenever a Cube script is called an exception trap is used to stop the model stream if an error occurs.

```
runtpp CTRAMP\scripts\preprocess\SetTolls.job
if ERRORLEVEL 2 goto done
runtpp CTRAMP\scripts\preprocess\SetHovXferPenalties.job
if ERRORLEVEL 2 goto done
runtpp CTRAMP\scripts\preprocess\CreateFiveHighwayNetworks.job
if ERRORLEVEL 2 goto done
```

## Step 4: Build non-motorized level-of-service matrices

The so-called "non-motorized" level-of-service matrices capture the distance to travel from a zone to every other zone by walking or bicycling. This distance is independent of congestion, which means the skims need only be built one time. This is done here, prior to executing an iteration of the travel model. The skims are built via a two step process using two Cube scripts as follows:

1. *CreateNonMotorizedNetwork.job* -- The non-motorized network is created via the following three steps: (a) start with all of the roadway links represented in the travel model; (b) exclude all freeway links; and, (c) add back in freeway links on bridges that have bicycle and pedestrian facilities, specifically the Golden Gate, Dumbarton, and Antioch bridges.
1. <strong>NonMotorizedSkims.job </strong>-- After preparing the network, the distance to traverse every potential zone-to-zone path in the Bay Area is stored in a matrix, separately for walking and bicycling. The intra-zonal distance is equal to 1/2 the distance to the nearest neighbor. Non-motorized travel times are computed via the UtilityExpressionCalculator files that define the choice models by assuming a fixed travel speed for both bicycling and walking.

The actual code is presented below.

```
runtpp CTRAMP\scripts\skims\CreateNonMotorizedNetwork.job
if ERRORLEVEL 2 goto done
runtpp CTRAMP\scripts\skims\NonMotorizedSkims.job
if ERRORLEVEL 2 goto done
```

##  Step 5: Prepare for iteration 0

The travel model is run iteratively, computing congested travel speeds, simulating individual choices, computing congested travel speeds, simulating individual choices, and on and on. Prior to simulating the first set of individual choices, congested travel speeds are computed based on user-specified demand. This step is referred to as "iteration 0". The trip tables fed into the initial assignment are stored in the *INPUT\warmstart* directory. The user can start with any level of demand. Doing this type of warm start analysis allows the travel model to converge more quickly to an equilibrium condition. However, because the model averages travel speeds across iterations (to force convergence), the choice of warm start demand is not arbitrary and should be selected with some care (e.g., demand from a year 2035 scenario should used to warm start a year 2035 scenario). Further, when comparing scenarios, each scenario should either (a) use the same set of "warm start" demand matrices or (b) confirm that each scenario converges to the same set of results with different warm start matrices (i.e. make sure the convergence point is the true point of convergence).

Prior to running each iteration, six DOS environment variables are set, as follows:

1. **ITER** -- for "iteration", this variable is used to label folders and output specific to this iteration;
1. **PREV_ITER** -- for "previous iteration", this variable specifies which network is to be part of the weighted average computation which determines the roadway volumes upon which congestion is estimated for the next iteration;
1. **WGT** -- for "weight", this variable specifies the weight applied in a weighted average computation for the volumes from this iteration's roadway assignment;
1. **PREV_WGT** -- "for previous weight", this variable specifies the weight applied in a weighted average computation for the volumes from the previous iteration's roadway assignment;
1. **SAMPLESHARE** -- for "sample share", this is the share of the synthetic population to be simulated in this iteration (in early iterations, a smaller share of the population may be required to adequately estimated congested speeds); and,
1. **SEED** -- for "random number seed", this variable allows the user to introduced stochastic variability into a single scenario (the software is set up to generate identical results across two runs executed with the same inputs on the same computer; if stochastic or simulation variability is desired, the random number seed can be changed via this variable).
Each iteration of the model generates estimates of freeway volumes. After the first iteration of the model, one set of volumes exist. These are then used to compute congested speeds which inform the choices for the second iteration of the model. After the second iteration of the model, two sets of volumes exist. These are averaged by the MTC travel model to create a set of volumes used to compute congested speeds which inform the choices for the third iteration of the model. The *WGT*, *ITER*, *PREV_WGT*, and <strong>PREV_ITER </strong>variables facilitate this calculation (as shown below in Steps 7 and 8). The actual code is shown directly below. During iteration 0, the choice models are not executed; the only action is to perform a highway assignment (see RunIterationBatch for details). As such, the <strong>SAMPLESHARE </strong>and <strong>SEED </strong>variables are not used. Because there are no other volumes from previous iterations for which a weighted average can be computed, the <strong>PREV_WGT </strong>and <strong>PREV_ITER </strong>variables are not used.

```
set ITER=0
set PREV_ITER=0
set WGT=1.0
set PREV_WGT=0.0
set SAMPLESHARE=0.00
set SEED=0
```

## Step 6: Execute the RunIterationBatch file

After setting the necessary parameters for an iteration through the model, the [[RunIterationBatch]] file performs all the travel model steps. The details of these steps are described on the [[RunIterationBatch]] file (the choice models depicted as items 2 through 5 on the [[ModelSchematic]] page are executed as part of a model iteration). The actual code is shown below.

```
call CTRAMP\RunIteration.bat
if ERRORLEVEL 2 goto done
```

## Step 7: Prepare for iteration 1 and execute the [[RunIterationBatch]] file

Using the congested speeds from the iteration 0 warm start exercise, an iteration of the model is now executed for the first full iteration. The steps in this process are as follows:

1. Set the <strong>ITER </strong>variable to 1 (this is the first iteration);
1. Set the <strong>PREV_ITER </strong>variable to 1, (the volumes are not averaged until the second iteration);
1. Set the <strong>WGT </strong>variable to 1.0, (the volumes are not averaged until the second iteration);
1. Set the <strong>PREV_WGT </strong>variable to 0.0 (the volumes are not averaged until the second iteration);
1. Set the <strong>SAMPLESHARE </strong>variable to 0.15 or some other number, depending on the application (for a standard scenario, MTC uses a 15 percent sample to get an initial estimate of congested speeds);
1. Set the <strong>SEED </strong>variable to any number (MTC uses zero);
1. Set the maximum number of shadow pricing iterations in the usual workplace location models to 4.

The first six steps in the above list follow from the above discussion on Step 5: Prepare for Iteration 0. The seventh step is performed to save a bit of run time. The usual workplace location sub-model selects a workplace for each worker in the synthetic population. After a single iteration of this sub-model, more workers "choose" to work in certain locations than their are employment opportunities. The sub-model is then executing again, this time introducing shadow prices (i.e. negative utilities) to employment locations in which the expected number of workers exceeded the number of jobs, thus reducing the attractiveness of these employment locations. The sub-model can be run iteratively until the number of workers is less than or equal to the number of employees in each zone. Here, we limit the number of iterations (to four) as computing the initial congestion levels (which is the purpose of the first iteration) does not require a precise match between workers and employment opportunities. The actual code to implement the above actions is shown below.

```
set ITER=1
set PREV_ITER=1
set WGT=1.0
set PREV_WGT=0.0
set SAMPLESHARE=0.15
set SEED=0

copy CTRAMP\runtime\mtcTourBased-master.properties CTRAMP\runtime\mtcTourBased.properties
echo. >> CTRAMP\runtime\mtcTourBased.properties
echo UsualWorkAndSchoolLocationChoice.ShadowPricing.MaximumIterations = 4 >> CTRAMP\runtime\mtcTourBased.properties

call CTRAMP\RunIteration.bat
if ERRORLEVEL 2 goto done
```

## Step 8: Prepare for iteration 2 and execute the RunIterationBatch file

Using the congested speeds from the first iteration, a second full iteration of the travel model is now performed. The steps in this process are as follows:

1. Set the <strong>ITER </strong>variable to 2 (this is the second iteration);
1. Set the <strong>PREV_ITER </strong>variable to 1 (the volumes from the second iteration run will be averaged with the volumes from the first iteration run to generate congested speed estimates for the third iteration);
1. Set the <strong>WGT </strong>variable to 0.50 (in the weighted average, the second iteration volumes have a weight of one-half);
1. Set the <strong>PREV_WGT </strong>variable to 0.50 (in the weighted average, the first iteration volumes have a weight of one-half);
1. Set the <strong>SAMPLESHARE </strong>variable to 0.25 or some other number, depending on the application (for a standard scenario, MTC uses a 25 percent sample to get a refined estimate of congested speeds);
1. Set the <strong>SEED </strong>variable to any number (MTC uses zero);
1. Use the shadow prices from the first iteration usual workplace location sub-model run as the initial shadow prices for second iteration usual workplace location sub-model run;
1. Set the maximum number of shadow pricing iterations in the usual workplace location sub-models to 2.

The above steps are the same as those discussed in Step 7: Prepare for Iteration 1 and Execute the [[RunIterationBatch]] file. The one minor difference is that an input file is being read in to "warm start" the usual workplace location sub-model. Here, we start with the shadow prices from the first iteration and further refine the estimates with two additional iterations of the usual workplace location sub-model. The actual code to implement the above actions is shown below.

```
set ITER=2
set PREV_ITER=1
set WGT=0.50
set PREV_WGT=0.50
set SAMPLESHARE=0.25
set SEED=0

copy CTRAMP\runtime\mtcTourBased-master.properties CTRAMP\runtime\mtcTourBased.properties
echo. >> CTRAMP\runtime\mtcTourBased.properties
echo UsualWorkAndSchoolLocationChoice.ShadowPricing.Input.File = main/ShadowPricing_3.csv >> CTRAMP\runtime\mtcTourBased.properties
echo UsualWorkAndSchoolLocationChoice.ShadowPricing.MaximumIterations = 2 >> CTRAMP\runtime\mtcTourBased.properties

call CTRAMP\RunIteration.bat
if ERRORLEVEL 2 goto done
```

## Step 9: Prepare for iteration 3 and execute the RunIterationBatch file

Using the congested speeds from the second iteration, a third full iteration of the travel model is now performed. The steps in this process are as follows:

1. Set the <strong>ITER </strong>variable to 3 (this is the third iteration);
1. Set the <strong>PREV_ITER </strong>variable to 2 (the volumes from the second iteration run will be averaged with the volumes from the second iteration run to generate congested speed estimates for the fourth iteration or the final speed estimates);
1. Set the <strong>WGT </strong>variable to 0.33 (in the weighted average, the third iteration volumes have a weight of one-third);
1. Set the <strong>PREV_WGT </strong>variable to 0.66 (in the weighted average, the second iteration volumes have a weight of two-thirds);
1. Set the <strong>SAMPLESHARE </strong>variable to 0.50 or some other number, depending on the application (for a standard scenario, MTC uses a 50 percent sample to get a final estimate of congested speeds);
1. Set the <strong>SEED </strong>variable to any number (MTC uses zero);
1. Use the shadow prices from the second iteration usual workplace location sub-model run as the initial shadow prices for third iteration usual workplace location sub-model run;
1. Set the maximum number of shadow pricing iterations in the usual workplace location sub-models to 2.

The above steps are the same as those discussed in Step 8: Prepare for Iteration 1 and Execute the [[RunIterationBatch]] ]file. The actual code to implement the above actions is shown below.

```
set ITER=3
set PREV_ITER=2
set WGT=0.33
set PREV_WGT=0.66
set SAMPLESHARE=0.50
set SEED=0

copy CTRAMP\runtime\mtcTourBased-master.properties CTRAMP\runtime\mtcTourBased.properties
echo. >> CTRAMP\runtime\mtcTourBased.properties
echo UsualWorkAndSchoolLocationChoice.ShadowPricing.Input.File = main/ShadowPricing_5.csv >> CTRAMP\runtime\mtcTourBased.properties
echo UsualWorkAndSchoolLocationChoice.ShadowPricing.MaximumIterations = 2 >> CTRAMP\runtime\mtcTourBased.properties

call CTRAMP\RunIteration.bat
if ERRORLEVEL 2 goto done
```

Please note that the [[RunModelBatch]] file can be configured to run any number of iterations of the travel model at any sampling rate. MTC does modify these parameters as the application needs change (this explanation is used to illustrate the how the model stream can be configured). For example, for a conformity run, MTC will perform a fourth iteration and use a 100 percent sampling rate. These changes can be made easily by modifying the [[RunModelBatch]] file and following the pattern of the previous iterations.

## Step 10: Assign transit trips to the transit network

The travel model system explicitly assumes that, contrary to the roadway network, transit service does not degrade (due to crowding) as transit use increases. Said another way, aside from the impact of roadway congestion on transit speeds, the representation of transit supply is independent of transit usage. As such, a transit assignment -- the process of identifying the specific routes that transit riders will use -- can be done only once, after the model system has reached a degree of convergence. This is done here by executing the Cube script *TransitAssign.job*. Please see the script file for complete details. The code to call this script is shown below.

```
call CTRAMP\scripts\assign\TransitAssign.job
if ERRORLEVEL 2 goto done
```

## Step 11: Build simplified skim databases

To facilitate analysis of travel outcomes using databases, MTC builds simplified, CSV databases from the more detailed and complete Cube skims. Details and specifications are described on the [[SimpleSkims]] page as well as in the <strong>SkimsDatabase.job </strong>script. The implementation code is shown below.

```
call CTRAMP\scripts\database\SkimsDatabase.job
if ERRORLEVEL 2 goto done
```

## Step 12: Directory clean up

Prior to ending the model run, the PATH variable is restored to its original condition, the Cube script log files are moved to the *\logs* directory, and temporary Cube script files are deleted. The implementation code is shown below.

```
set PATH=%OLD_PATH%
copy *.prn logs\*.prn
del *.script.*
del *.script
```


-- Main.LisaZorn - 28 Apr 2017