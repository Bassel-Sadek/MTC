[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[RunModel]]

---

# Run the Model

This page provides instructions for executing the travel model. For a description of the underlying computing environment, see the [[ComputingEnvironment]] page; for a general description of the underlying system design, see the [[SystemDesign]] page; for a description of the configuration files likely needing to be modified before executing the model, see the [[SetupConfiguration]] page.

These instructions are for the simplified single-server run that we're running these days.  We used to run across several nodes but now we run the model on a single machine.

## Step 1: Execute the RunModelBatch file

MTC runs the model by calling a series of commands stored in an MS-DOS batch file named [**RunModel.bat**](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/model-files/RunModel.bat). An overview of the steps performed by this batch file are noted below; complete details are provided on the [[RunModelBatch]] page. The current MTC implementation runs three full iterations of the models (i.e. speeds are fed back through the entire model stream, meaning steps 2 through 5 on the [[ModelSchematic]]); the **RunModel.bat** file can be easily configured to run any number of iterations.

* Sets the necessary path variables as described on the [[SetupConfiguration]] page;
* Starts up the Cube Voyager nodes
* Builds a set of distance-based non-motorized skims that are not modified across feedback iterations;
* Iteration 0:
  * Assigns a set of "warm start" trip tables to the highway network and creates skims
* Iterations 1-3:
  * Sets the parameters for the iteration 1 and call the **RunIteration.bat** file ([[RunIterationBatch]]), which performs the following steps:
   * Builds highway and transit skims;
   * Executes the CT-RAMP choice models;
   * Executes the freight models;
   * Performs highway assignment;
   * Sets the parameters for iteration 2 and calls the **RunIteration.bat** file ([[RunIterationBatch]]);
   * Sets the parameters for iteration 3 and calls the **RunIteration.bat** file ([[RunIterationBatch]]);
   * Performs transit assignment
   * Notifies our slack channel that the iteration is complete
* Create destination choice logsums
* Summarization steps
* Shuts down the Cube Voyager nodes as and the java processes
* Notifies our slack channel that the model run is complete

