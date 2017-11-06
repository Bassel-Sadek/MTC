[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[SystemDesign]]

***

# System Design

On this page, the manner in which the software is configured to take advantage of the hardware is described (see the ComputingEnvironment page for details on the hardware and software used in the travel model; see the [[SetupConfiguration]] page for details on setting up and configuring the MTC to run on a given set of hardware).

## Distributed Computing

The MTC travel model uses two types of distributed applications. The first is facilitated by the Cube Cluster software and allows the skim building and assignment steps to utilize multiple threads. The second is facilitated by the CT-RAMP software, which allows the choice models to be distributed across multiple threads and multiple computers. An overview of both of these applications is provided below.

### Cube Cluster

Citilabs Cube scripts facilitate two types of distribution, both of which are highly configurable through the Cube scripting language and the Cube Cluster thread management system. Cube scripts allow for two distinct types of multi-threading, as follows:
1. Intra-step threading: The DistributeINTRAStep keyword keyword allows calculations that are performed across a matrix of data to be performed in blocks -- specifically rows of data -- across multiple threads. MTC uses intra-step threading in highway assignment, allowing shortest paths to be constructing for more than one origin at a time. Complex matrix calculations can also benefit from intra-step threading.
2. Multi-step threading: The DistributeMULTIStep keyword allows blocks of code to be distributed across multiple threads. For example, if the same calculations are being performed for five different time periods, the same block of code (with variables) can be distributed across computers for parallel processing. This type of Cube multi-threading is a bit less flexible than the intra-step threading as it requires threads to be identified _a priori_ (e.g., thread one will do the calculations for time period A), where the intra-step threading can be given a list of available processes and use what is available. MTC uses multi-step threading for highwway skimming, transit skimming, highway assignment, the conversion of trip lists to trip matrices, highway assignment, and transit assignment.

As noted in the [[ComputingEnvironment]] page, the MTC travel model specifies the Cube scripts to take advantage of 48 threads. A knowledgeable user can easily adjust the necessary scripts to take advantage of more or fewer processors.

### CT-RAMP

The CT-RAMP Java software allows for the choice models to be distributed across threads and machines. The MTC application currently uses one machine, but the CT-RAMP software can be configured fairly easy to utilize fewer or more machines. CT-RAMP uses the [Java Parallel Processing Framework](http://www.jppf.org/), or JPPF, to manage the distribution of tasks. JPPF is an open-source Java package. As illustrated in the figure below, the JPPF framework consists of three main parts as follows: (i) a driver, also referred to as the JPPF server; (ii) one or more nodes, typically one node is established on each machine; (iii) a client, the CT-RAMP software in this case.

As noted on the [[ComputingEnvironment]] page, MTC uses one computer. The JPPF driver process is executed on this computer and acts like a traffic cop by acquiring tasks from the client and distributing those tasks to the node processes. When the node processes complete tasks, the results are returned back to the client via the JPPF driver. One node is used in the MTC application. After being created, the node listens for tasks from the JPPF driver.

![](https://github.com/BayAreaMetro/modeling-website/blob/master/foswiki_imgs/JPPF_Workflow.png)

Node processes receive tasks, perform those tasks, and return the results. Nodes are configured to communicate with the driver process when they are started. MTC configures the nodes to use 66 GB of memory and 24 threads (see the [[SetupConfiguration]] page for details on where these parameters are specified). The JPPF driver attempts to balance computational loads across available nodes. The driver also retrieves class files, i.e. sets of Java code, from the client application and passes those to the nodes as needed.

The CT-RAMP software, which serves as the client, is responsible for creating task objects that can be run in parallel and submitting those to the driver. Because the MTC travel model simulates households, the CT-RAMP software creates packets of 5,000 households and sends those packets to the nodes for processing. As the nodes complete tasks and returns them to the driver, the driver gives the nodes new tasks, attempting to keep each node uniformly busy.

## Household Manager and Matrix Manager

Before executing a model run, the travel model requires a Household Manager and a Matrix Manager be created. In the MTC application. The Household Manager is tasked with managing the simulated households, as well as each simulated person in each simulated household. The Household Manager provides the JPPF nodes with information regarding the households for which the JPPF nodes are applying choice models and stores the resulting information computed by the JPPF nodes. To help keep run time down, the synthetic population is read from disk and stored in memory at the beginning of the application and then continuously updated as choice models are completed and iterations are performed. When the last iteration is complete, the necessary information is written to disk.

The Matrix Manager is tasked with managing all of the skim matrices used by the choice models. When a skim is needed, a request is made to the Matrix Manager, which then reads the required skim from disk and stores it in memory. Once in memory, each matrix is available to any other JPPF node process that may need it.

Both the Household Manager and Matrix Manager have substantial memory footprints.

-- Main.DavidOry - 27 May 2016
