[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[ComputingEnvironment]]

***

# Computing Environment
The hardware and software MTC uses to execute _Travel Model One_ are described on this page. To date, MTC has not experimented enough with the model to define the minimum or ideal hardware configuration. As such, the description here is for a hardware set up that is sufficient. It is important to note that both the software and model structure are highly configurable and flexible; depending on the analysis needs, the required computing power could vary dramatically.

## Hardware

MTC uses a single server with the following characteristics:
   1 Operating system: Microsoft Windows Server 2012 R2 Standard, 64-bit;
   1 Processors: Two Intel Xeon E5-2680 v3 @ 2.50 GHz (24 cores, 48 logical processors);
   1 Memory (RAM): 256.0 GB

## Software

The following software are required to execute the MTC travel model.

### Citilabs Cube Voyager
The travel model currently uses version 6.4.2 of [Citilabs](http://citilabs.com/) Cube software. The Cube software is used to build skims, manipulate networks, manipulate matrices, and perform assignments.

### Citilabs Cube Cluster
The Cube Cluster software allows for the Cube scripts to be multi-threaded. In the current approach, the travel model uses 48 computing nodes. However, the Cube scripts can be manipulated to use any number of computing nodes across any number of machines, provided each machine has, at a minimum, a Cube Voyager node license. Cube Cluster is not strictly necessary, as the Cube scripts can be modified to use only a single computing node. Such an approach would dramatically increase run times.

### Java and CT-RAMP

MTC's travel model operates on the open-source Coordinated Travel - Regional Activity-based Modeling Platform (or CT-RAMP) developed by [Parsons Brinckerhoff](http://pbworld.com/). The software is written in the [Java](http://java.com/en/) programming language. Because the CT-RAMP software compiles code "on-the-fly", the 64-bit Java Development Kit (version 1.7) must be installed on each computer running the CT-RAMP software. The Java Development Kit includes the Java Runtime Environment. The 64-bit version of the software allows CT-RAMP to take advantage of larger memory addresses.

### GAWK

Certain text file manipulations are handled in the travel model using the free [GAWK](http://www.gnu.org/software/gawk/) software. GAWK must be installed on the computer executing the Cube scripts.

### Microsoft Excel

The CT-RAMP software allows discrete choice models to be specified via so-called UtilityExpressionCalculators. These files are Excel-based.

### Python

[Python 2.7](https://www.python.org/) is used to execute a variety of utility functions. Please see the MTC GitHub repo [here](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/utilities/python-install/go_go_python.bat) for the Python packages used in Version 0.5 of the model.

Please note that a variety of model utility scripts also use R and Tableau.

-- Main.DavidOry - 27 May 2016
