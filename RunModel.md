[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[RunModel]]

---

# Run the Model

This page provides instructions for executing the travel model. For a description of the underlying computing environment, see the [[ComputingEnvironment]] page; for a general description of the underlying system design, see the [[SystemDesign]] page; for a description of the configuration files likely needing to be modified before executing the model, see the [[SetupConfiguration]] page.

These instructions are for the simplified single-server run that we're running these days.  We used to run across several nodes but now we run the model on a single machine.

## Step 1: Start Cube Cluster
The Cube Cluster software allows for the Cube scripts to be multi-threaded. In MTC's current setup, 48 computing nodes are used. The steps to start these nodes are as follows:
* Launch the Cube Cluster software
* Select "1-48" under "Process List"
* Check the "Hide New Nodes" option to minimize the number of pop-up windows
* Click "Start Nodes"

To double check that the nodes are started, expand the small upwards facing arrow on the task bar at the bottom-right of the screen. One should see 48 Cube icons.

## Step 2: Execute the RunModelBatch file

MTC runs the model by calling a series of commands stored in an MS-DOS batch file named [**RunModel.bat**](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/RunModel.bat). An overview of the steps performed by this batch file are noted below; complete details are provided on the [[RunModelBatch]] page. The current MTC implementation runs three full iterations of the models (i.e. speeds are fed back through the entire model stream, meaning steps 2 through 5 on the [[ModelSchematic]]); the **RunModel.bat** file can be easily configured to run any number of iterations.

* Sets the necessary path variables as described on the [[SetupConfiguration]] page;
* Creates a working folder structure under the **M:\{Project}** directory and copies the INPUT files to the working folders;
* Assigns a set of "warm start" trip tables to the highway network;
* Builds a set of distance-based non-motorized skims that are not modified across feedback iterations;
* Sets the parameters for iteration 1 and calls the **RunIteration.bat** file ([[RunIterationBatch]]), which performs the following steps:
   * Builds highway and transit skims;
   * Executes the CT-RAMP choice models;
   * Executes the freight models;
   * Performs highway assignment;
   * Sets the parameters for iteration 2 and calls the **RunIteration.bat** file ([[RunIterationBatch]]);
   * Sets the parameters for iteration 3 and calls the **RunIteration.bat** file ([[RunIterationBatch]]);
   * Performs transit assignment.

The **RunModel.bat** file will pause and prompt you to start the java processes:

`Project Directory updated.  Please start java processes (main and nodes) and press Enter to continue...`


At this point, do Steps 3a and 3b and then press Enter to continue.

## Step 3a: Start the Household Manager, Matrix Manager, JPPF Driver, and Cube Cluster

To do this, first navigate to **M:\{Project}\CTRAMP\runtime** (where {Project} is a scenario-specific directory) on the computer from which you want to run the Household Manager, Matrix Manager, JPPF driver, and Cube scripts, then double click on [**JavaOnly_runMain.cmd**]([https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/runtime/JavaOnly_runMain.cmd). This command will cause the following actions:
* The Household Manager Java process will start, appearing as a DOS window;
* The Matrix Manager Java process will start, appearing as a DOS window;
* The JPPF Driver Java process will start, appearing as a DOS window.

## Step 3b: Start a JPPF worker node

Start the [**JavaOnly_runNode0.cmd**](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/runtime/JavaOnly_runNode0.cmd) batch file by navigating to the **M:\{Project}\CTRAMP\runtime** directory, then by double-clicking on on the script. This command will launch a JPPF node Java process, appearing as a DOS window.

## Step 3: After the model completes, kill Java processes and Cube Cluster to prepare for next model run

After a model run is complete, the Household Manager, Matrix Manager, JPPF Driver, Cube Cluster nodes, and each JPPF node will still be operating and using memory. To stop these processes, close their respective windows.
 

-- Main.LisaZorn - 28 Apr 2017