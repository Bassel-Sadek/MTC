[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[SetupConfiguration]]

----

# Setup and Configuration

This page provides details on setting up the travel model to run on a cluster of computers, including descriptions of the necessary configuration files.

## Step 1: Create the required folder structure

The MTC travel model is delivered as a compressed folder containing two directories, `CTRAMP` and `INPUT` and one [MS DOS batch file](http://en.wikipedia.org/wiki/MS-DOS_batch_files), [`RunModel.bat`](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/RunModel.bat). These files can be placed in any directory on a computer designated as the main controller of the program flow. On MTC's set up, these files are placed on the _mainmodel_ computer (see [[SystemDesign]] page for more details).

The `CTRAMP` directory contains all of the model configuration files, Java instructions, and Cube scripts required to run the travel model, organized in the following three folders:
   * <strong><a href="https://github.com/MetropolitanTransportationCommission/travel-model-one/tree/master/model-files/model" target="_blank">model</a> </strong>-- contains all of the UtilityExpressionCalculator files that specify the choice models;
   * <strong><a href="https://github.com/MetropolitanTransportationCommission/travel-model-one/tree/master/model-files/runtime" target="_blank">runtime</a> </strong>-- contains all of the Java configuration and JAR (executable) files, as well as the files necessary for Java to communicate with Cube;
   * <strong><a href="https://github.com/MetropolitanTransportationCommission/travel-model-one/tree/master/model-files/scripts" target="_blank">scripts</a> </strong>-- contains all of the Cube scripts and associated helper files.

The <strong>INPUT </strong>directory contains all of the InputFiles required to run a specific scenario. When configuring the model on a new computing system, one should make sure that the results from an established scenario can be recreated before developing and analyzing a new scenario. The <strong>INPUT </strong>directory contains the following folders:
   * <strong>hwy </strong>-- contains the input free flow highway network, which is named, by convention, *freeflow.net* (see the HighwayNetworkCoding page for details);
   * <strong>trn </strong>-- contains all of the input transit network files organized across three directories, namely: *transit_lines*, *transt_fares*, and *transit_support* (see the TransitNetworkCoding page for details);
   * *landuse* -- contains the socio-economic input land use file (described on the TazData page) and walk shares file;
   * <strong>nonres </strong>-- contains the fixed, year-specific internal/external trip tables, the fixed, year-specific air passenger trip tables, and files used to support the commercial vehicle model;
   * <strong>popsyn </strong>-- contains the synthetic population files per the formats described on the PopSynHousehold and PopSynPerson pages.
The <strong>RunModel.bat </strong>contains a list of MS-DOS instructions that control model flow.

*Update:* In order to track the sources of `INPUT` files and `CTRAMP` files, MTC staff has begun using a setup script to setup the model to run.  The current version of this is [`SetUpModel_PBA50.bat`](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/SetUpModel_PBA50.bat).

### Verify and update paths in SetPath.bat

Configuration specific to the locations of libraries and executables have been consolidated in the [ SetPath.bat](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/runtime/SetPath.bat) file.  The version on GitHub is the current version that we use.

Note that the `TPP_PATH` includes the location that [Cube Voyager] is installed as well as the **VoyagerFileAPI**, which is a DLL library needed by the CTRAMP core so that its Matrix Manager can read Cube matrix files. 

### RuntimeConfiguration.py

[RuntimeConfiguration.py](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/scripts/preprocess/RuntimeConfiguration.py) is meant to do the remainder of the runtime-setup automatically, so that all the configuration is in one place and done automatically.  See the script for details.

Now that the model is configured, the user can run the model; the steps required to do so are described on the RunModel page.
 