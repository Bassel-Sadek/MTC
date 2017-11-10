[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[NetworkCoding]] > [[TransitNetworkCheck]]

---

```diff
- This process is somewhat outdated.
- See https://github.com/BayAreaMetro/travel-model-one/tree/master/utilities/check-network
```

Two network check scripts can be run to ensure the transit network is ready for use. The first check builds the transit network to ensure the highway and transit networks are consistent (i.e. a node isnt missing in one file for example). The second check ensures the TP+ block files reference all of the input files that make up the network.
1. [Transit Line Files Checks](TransitNetworkCheck#1-transit-line-files-tpl-checks)
1. [Transit Block Files Checks](TransitNetworkCheck#2-transit-block-files-block-checks)

## 1. Transit Line Files (.TPL) Checks

The [transit line files](TransitNetworkCoding#2-transit-line-files) are coded on top of the highway networks and these two networks need to be consistent. There are many ways to check for the consistency between the transit line files and highway network files. The simplest way is to build a transit network file via the [**buildTransitNetworks.job**](TransitNetworkCoding#script-buildtransitnetworkjob) script. If the network is successfully built then it confirms the consistency between the highway and transit files. If the build fails, then TP+ will create a print file with a list of errors. Following are some typical inconsistencies and errors:

1. All transit nodes must exist in the highway network or be specified in the support line files. Figure 1 shows the error message for this error.
1. The transit node sequence should follow the same node sequence as in the highway networks. Figure 2 shows the error message for this error.
1. Transit stops cannot be specified more than once for the same line. Figure 3 shows the error message for this error.

*Figure 1 Transit Nodes Not in Highway Network*

![Transit Nodes Not in Highway Network](https://raw.githubusercontent.com/BayAreaMetro/modeling-website/master/foswiki_imgs/Check_transit_nodes.jpg)

*Figure 2 All Transit Nodes Exist in Highway Network but not Coded in Correct Sequence*

![All Transit Nodes Exist in Highway Network but not Coded in Correct Sequence](https://raw.githubusercontent.com/BayAreaMetro/modeling-website/master/foswiki_imgs/Check_transit_nodes_seq.jpg)

*Figure 3 Transit Stop Node Specified Twice in a Same Line*

![Transit Stop Node Specified Twice in a Same Line](https://raw.githubusercontent.com/BayAreaMetro/modeling-website/master/foswiki_imgs/Check_transit_stops.jpg)

## 2. Transit Block Files (.BLOCK) Checks

A second check can be done to ensure consistency among the TP+ [line block files](TransitNetworkCoding#2-transit-line-files). A block file is a block of script that exists as a separate file and consists of lines of code or other specifications that are called by a main script. In order to keep from changing the main script every time a new operator or fare specification is added, these line and fare specifications are moved to block files. The block files refer to separate line and fare files that actually define the lines and fares.

### 2.1 Transit Line Block File

Each transit line file (*.tpl) is named by operator name and line-haul mode type. A number of transit line files therefore need to be read by TP+ when building the transit network. Instead of specifying the individual transit line files, a block file is specified, which consists of all the transit line files. Whenever a new transit file (.TPL) is developed, it needs to be referenced in the transit block file as well. As a result, there is a chance of omitting the transit line files in the block file. The following script checks for consistency among the *tpl files in a folder and what is specified in the block file.

#### Script CheckTransitLineBlock.job

This scripts checks for the following:
1. Whether all the TPL files are correctly specified in the transit block file.
1. Whether there are any commented out transit block lines that correspond to existing TPL files.
1. Whether there are TPL files that do not exist but that are specified in the block file Table 1 shows the input and outputs used in the script and Figure 4 shows the output files.
The script outputs the following information:
1. List all files specified in the Transit Block File
1. Lists all TPL files found in the directory
1. Generates a binary code:
   1. Match = 1, TPL file exists and is referenced in the Transit Block File
   1. Match = 0, Either the TPL file doesnt exist or exists but is not specified in the block file
1. Lists TPL files that do not exist but are specified in Transit Block File
1. Lists TPL files that exist but are not specified in Transit Block File

*Table 1 Input and Output Files of Block File Check Script*

| Inputs/ Outputs | Name | Description | Examples |
|---|---|---|---|
|  I  | Transit Line Block File | Block File with All the Listed Transit Lines | Transit_Lines.block |
|  I  | Transit Line Files in Directory | Transit Line Files in the Directory | AC_LOCAL.tpl |
|  O  | Output Log File | Compares Transit Block File to TPL files in the directory | Compare_transit_lines.txt |


*Figure 4 Transit Line Block Comparison (Compare_transit_lines.txt)*

![Transit Line Block Comparison](https://raw.githubusercontent.com/BayAreaMetro/modeling-website/master/foswiki_imgs/Compare_transit_block_lines.jpg)


### 2.2 Transit Fare Block File

The transit fare block file is similar to the transit line block file. However, the direct fares, transfer fares and link fares are directly specified in the script and only the station-to-station fare files are specified as a block file (see section Transit Fare Files for more details on transit fare types). Whenever a new station-to-station fare file is developed it also needs to be referenced in the transit fare block. The following script checks whether all the station-to-station fare files are specified in the block file.

#### Script CheckTransitFareBlock.job

This scripts checks for the following:
   1 Whether all the FAR files are correctly specified in the transit fare block file
   1 Whether there are any commented out transit fare block lines that correspond to existing FAR files
   1 Whether there are FAR files that do not exist but are specified in the fare block file
Table 2 shows the input and outputs used in the script and Figure 5 shows the outputs. The script outputs the following:
   1 List all fare files specified in the Transit Block File
   1 Lists all FAR files found in the directory
   1 Generates a binary code:
      1 Match = 1, The FAR file exists and is referenced in the Transit Fare Block Fileb.
      1 Match = 0, Either the FAR file doesnt exist or exists but is not specified in the fare block file
   1 Lists FAR files that do not exist but are specified in Transit Fare Block File
   1 Lists FAR files that exist but are not specified in Transit Fare Block File

*Table 2 Input and Output Files of this Script*

| Inputs/ Outputs | Name | Description | Examples |
|---|---|---|---|
|  I  | Transit Fare Block File | Block File with All the Listed Transit Lines | Transit_Faremat.block |
|  I  | Transit Fare Files in the Directory | Transit Fares Files in the Directory | ACE.FAR |
|  O  | Output Log File | Compares Transit Fare Block File to FAR files in the directory | Compare_transit_farefiles.txt |
 

*Figure 5 Transit Fare Block Comparison (Compare_transit_farefiles.txt)*

![Transit Fare Block Comparison](https://raw.githubusercontent.com/BayAreaMetro/modeling-website/master/foswiki_imgs/Compare_transit_farefiles.jpg)
