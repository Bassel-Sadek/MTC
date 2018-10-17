[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[NetworkCoding]] > [[HighwayNetworkCoding_Old]]

***

**Saving this as archive to HighwayNetworkCoding_Old for reference. -lmz 2018/20/17**

***

The MTC highway network is coded and maintained as a comprehensive highway network file, commonly referred to as the *master highway network*. The file consists of network links that represent the roadways. A *project highway network* file is developed in three stages from the master highway network file. It consists of roadway links classified by functional class, zone connector links, and a few other additional links to support transit modeling. A project-specific highway network is developed as follows:

1. [Start with the master network file](HighwayNetworkCoding#1-master-network)
1. [Create a new project in the master highway network](HighwayNetworkCoding#2-create-a-new-project-in-the-master-network)
1. [Extract a project specific (base) highway network from the master highway network](HighwayNetworkCoding#3-extracting-a-project-network-from-the-master-network)
1. [Create highway networks by time-of-day](HighwayNetworkCoding#4-creating-highway-networks-by-time-of-day)

Once a project-specific highway network is extracted from the master network, the [transit background network](TransitNetworkCoding#transit-background-files) is created. The transit background network is later used in [creating the transit network](TransitNetworkCoding).

## 1. Master Network

The master highway network consists of all the highway links for all projects. In the master network file, the analyst codes each link with attributes common to all projects, (such as distance) and also codes each link with the project-specific attributes such as area type, facility type, and number of lanes. Table 1 shows the list of project-specific variables in the master highway network. The attribute table lists the possible values for each of the project-specific variables.

*Table 1 Project Specific Link [Attribute Table](MasterNetworkLookupTables)*

| Attribute | Description | Example Attribute Name {Values} |
|-----------|-------------|---------------------------------|
| LANE{Project} | Number of Lanes | laneRTP2040Base {0,1,2,3,---} |
| [TOS](MasterNetworkLookupTables){Project} | Special Speed Capacity | TOSRTP2040Base {0,1,2,3,---} |
| [SIG](MasterNetworkLookupTables){Project} | Signal Specific Lane | SIGRTP2040Base {0,1,2,3,---} |
| [USE](MasterNetworkLookupTables){Project} | User Class Type | USERTP2040Base {0,1,2,3,---} |
| [TCLASS](MasterNetworkLookupTables){Project} | Toll Class Type | TCLASSRTP2040Base {0,1,2,3,---} |
| [HOT](MasterNetworkLookupTables){Project} | High Occupancy Toll | HOTRTP2040Base {0,1,2,3,---} |
| [FT](MasterNetworkLookupTables){Project} | Facility Type | FTRTP2040Base {0,1,2,3,---} |
| [AT](MasterNetworkLookupTables){Project} | Area Type | ATRTP2040Base {0,1,2,3,---} |
| [BRT](MasterNetworkLookupTables){Project} | Exclusive BRT Lanes | BRTRTP2040Base {0,1,2,3,---} |

At the beginning of a new project, the analyst must check the master network to determine if the appropriate links and link attributes exists in the master network for that specific project. If the links and/or link attributes do not exist or do not represent the project, then the analyst must code the appropriate links and their attributes into the master network. The analyst must keep the master network up to date by adding new highway links and variables that define the latest projects.

## 2. Create a New Project in the Master Network

The analyst first must check the master network for the project-specific links and variables. If the project is not defined then the analyst must add new links to the master network, usually by copying and pasting similar nearby links. After creating a new link, the analyst must set the project-specific attributes defined in Table 1. To do this, the analyst must run the script [RTP2040_Base.job](HighwayNetworkCoding#21-script-rtp2040_basejob) to create a new set of project-specific link variables in the master network that they then edit the attributes that are specific to the project.

### 2.1 Script RTP2040_Base.job

This script adds a new set of project-specific variables to the highway network by duplicating a set of project-specific variables and renaming them with the user specified (i.e. current) project name. Table 2 shows the list of new variables added to the master highway network file and Table 3 lists the input and output files of the script. The analyst is required to run this script only to update the master network file before exporting the project-specific network.

*Table 2 Project Specific Variables Added by RTP2040_Base.job*

| Attribute | Description | Example Attribute Name {Values} |
|-----------|-------------|---------------------------------|
| LANE{CurrentProject} | LANE{CurrentProject} = LANE{Old} | 2 |
| FT{CurrentProject} | FT{CurrentProject} = FT{Old} | 3 |
| TOS{CurrentProject} | TOS{CurrentProject} = TOS{Old} | 0 |
| HOT{CurrentProject} | HOT{CurrentProject} = HOT{Old} | 1 |
| SIG{CurrentProject} | SIG{CurrentProject} = SIG{Old} | 0 |
| USE{CurrentProject} | USE{CurrentProject} = USE{Old} | 1 |
| TCLASS{CurrentProject} | TCLASS{CurrentProject} = 0 | 0 |

Note that the TCLASS{CurrentProject} variable is coded as zero as it needs to be changed manually based on the project

*Table 3 Input and Output Files of RTP2040_Base.job*

| Input/Output | Description | Example |
|---|----------------------------|------------------------------------|
| I | Old Master Highway Network | MASTER_NETWORK_December22_2010.NET |
| O | New Master Highway Network | MASTER_NETWORK_March30_2011.NET |

## 3. Extracting a Project Network from the Master Network

After creating project specific links and attributes in the master highway network, the analyst extracts a project specific network with the scripts [Create 2040_Base.job](HighwayNetworkCoding#31-script-create-2040_basejob) and [Network_Update_Modified.job](HighwayNetworkCoding#32-script-network_update_modifiedjob).

### 3.1 Script "Create 2040_Base.job"

This script extracts the project-specific highway network from the master network. The script creates a project-specific highway network from the master highway network with only the required attributes shown in Table 4. All of the project-specific attributes are renamed to drop the project name suffix and links with the setting LANE=0 are excluded during the extracting process. Many of the attributes are empty at this point since their value has yet to be calculated. Table 5 lists the input and output files of the script.

*Table 4 Project Specific Link Attributes*

| Variable | Description | Example |
|----------|-------------|---------|
| A | From node | 20298 |
| B | To node | 20300 |
| DISTANCE | Link Distance (miles) | 14.1 |
| SPDCLASS | Speed Class Type | 19 |
| CAPCLASS | Capacity Class Type | 19 |
| ROUTENUM | ?? | 238 |
| AUX | ?? | 0 |
| YEAR | Year | 0 |
| FFS | Free Flow Speed | 60 |
| FFT | Free Flow Time | 14.1 |
| FT2000 | Facility Type in Year 2000 | 2 |
| GL | County Code | 4 |
| LANES | Number of Lanes | 2 |
| TOLLCLASS | Toll Class Type | 0 |
| USE | User Class Type | 1 |
| OT | Observed Time for Toll Queuing Links | 0 |
| CAP | Capacity Per Lane | 1950 |
| AT | Area Type | 3 |
| FT | Facility Type | 2 |
| TOS | Special Speed Capacity | 1 |
| HOT | High Occupancy Toll | 0 |
| TSIN | Time-based link | 1 |
| SIGCOR | Signal coordinated link | 1 |

*Table 5 Input and Output Files of Create 2040_Base.job*

| Input/Output | Description | Example |
|--------------|-------------|---------|
| I | Master Highway Network | MASTER_NETWORK_December22_2010.NET |
| O | Project Specific Highway Network | Year2040_Base_NETWORK_December22_2010_w.NET |

### 3.2 Script "Network_Update_Modified.job"

This script updates the project-specific highway network file with calculated attributes and writes out a new highway network file. The primary calculated attributes are capacity and free flow speed, but other attributes are set as well as shown in Table 6. The analyst is required to run this script after running the [Create 2040_Base.job](HighwayNetworkCoding#31-script-create-2040_basejob) script. Table 7 shows the input and output files of the script.

*Table 6 Highway Network Calculated Link Attributes*

| Variable | Description | Example |
|----------|-------------|---------|
| METER | Ramp meter present, set If(FT2000=8) | 1 |
| FT | Facility type modified IF (FT=8) FT=5 | 2 |
| FT2000 | Facility type in year 2000 modified IF (FT2000=8) FT2000=5 | 2 |
| CAPCLASS | Capacity class type, set by [AT](MasterNetworkLookupTables), [FT](MasterNetworkLookupTables), [TOS](MasterNetworkLookupTables) and SIGCOR type lookup | 19 |
| FFS | Free flow speed, set by CAPCLASS | 60 |
| CAP | Capacity per lane, set by CAPCLASS | 1950 |
| FFT | Free flow time, calculated as (DISTANCE/FFS)*60 or as OT, IF(TSIN=1 & TOLLCLASS=1-100) | 14.1 |
| OT | Observed time, set to FFT If(TSIN=1 & TOLLCLASS=0) | 3.5 |
 

*Table 7 Input and Output Files of Network_Update_Modified.job*

| Input/Output | Description | Example |
|--|--|--|
| I | Project Specific Highway Network | Year2040_Base_NETWORK_December22_2010_w.NET |
| O | Output Updated Project Specific Highway Network | Year2040_Base_NETWORK_December22_2010.NET |

## 4. Creating Highway Networks by Time of Day

After creating the project specific network file, the analyst must create the highway network files by time-of-day. This is done in two stages:
1. The analyst adds five sets of toll values to each link in the network where each set represents one of the five time periods shown in Table 8 and each set includes toll values for each user class.
1. The analyst runs the script to create five highway networks by time-of-day.

All tolls should be expressed in year 2000 cents. The scripts to do these two steps are: [SetTolls.job](HighwayNetworkCoding#41-script-settollsjob) followed by [CreateFiveHighwayNetworks.job](HighwayNetworkCoding#42-script-createfivehighwaynetworksjob).

*Table 8 Highway Network Time Periods*

| &lt;timeperiod&gt;Code | Name | Hours |
|--|--|--|
| EA | Early AM | 3am to 6am |
| AM | AM Peak Period | 6am to 10am |
| MD | Midday | 10am to 3pm |
| PM | PM Peak Period | 3pm to 7pm |
| EV | Evening | 7pm to 3am |


### 4.1 Script "SetTolls.job"

Before creating the time-of-day networks, but after creating the project-specific network, the analyst then updates the bridge and value tolls. Bridge tolls are the tolls charged at the bridges and value tolls are tolls paid to save time by shifting to an alternative facility (e.g. HOT) or nearby facility. Each of the eight existing Bay Area bridge toll booths links has a unique TOLL coded as shown in Table 9. All tolls should be expressed in year 2000 cents. To change a toll value, the script must be changed.

*Table 9 Bay Area Bridge Toll Class*

| Toll Class Code | Bay Area Bridge | Example |
|--|--|--|
| 1 | Benicia-Martinez Bridge | If (A = 11597 & B = 11683) TOLL = 0 |
| 2 | Carquinez Bridge | If (A = 11667 & B = 11634) TOLL = 0 |
| 3 | Richmond Bridge | If (A = 2341 & B = 2357) TOLL = 0 |
| 4 | Golden Gate Bridge | If (A = 7319 & B = 7338) TOLL = 0 |
| 5 | San Francisco/ Oakland Bay Bridge | If (A = 2784 & B = 2802) TOLL = 0 |
| 6 | San Mateo Bridge | If (A = 3642 & B = 3649) TOLL = 0 |
| 7 | Dumbarton Bridge | If (A = 3895 & B = 3896) TOLL = 0 |
| 8 | Antioch Bridge | If (A = 1673 & B = 1621) TOLL = 0 |
| 9* | Reserved for New Bridges |   |
| 10* | Reserved for New Bridges |   |
| 11* | Reserved for Value tolls which are used by HOT lanes and are defined in hwyParam.block |   |

*Note that Toll Classes 9-11 are reserved for new bridges and test case scenarios.

The attribute TOLL is a legacy attribute and is no longer output by this script. Instead, TOLL is set first, then a new attribute TOLLCLASS is set to TOLL. The attribute TOLLCLASS then becomes the output. A separate toll can be specified for each vehicle class. The vehicle class link toll link attributes are shown in Table 10. A separate toll can be specified for each vehicle class, as shown in Table 11. Table 12 shows the inputs and outputs of this script.

*Table 10 Toll User Class Specific Link Attributes*

| &lt;userclass&gt;Code | Description | Example |
|--|--|--|
| DA | Drive alone, SOV | 200 |
| S2 | Shared ride two, HOV2 | 150 |
| S3 | Shared ride three plus, HOV3+ | 100 |
| VSM | Very small commercial trucks, which are assumed to be two-axle vehicles | 100 |
| SML | Small commercial trucks, which are assumed to be two-axle vehicles | 100 |
| MED | Medium commercial trucks, which are assumed to be three-axle vehicles | 100 |
| LRG | Combination trucks, which are charged the average of the five- and six-axle fee | 100 |


*Table 11 Output Toll Class Link Attributes*

| Variable | Description | Example |
|--|--|--|
| TOLL&lt;timeperiod&gt;_&lt;userclass&gt; | Bridge and Value Tolls by User Class and Time of Day | TOLLEA_DA = 200 |
| TOLLCLASS | Replaces TOLL values with TOLLCLASS | TOLLCLASS = TOLL |


*Table 12 Input and Output Files from this Script*

| Input/Output | Description | Example |
|--|--|--|
| I | Updated Project Specific highway Network | freeflow.net |
| O | Highway Network with Toll values | withTolls.net |

### 4.2 Script "CreateFiveHighwayNetworks.job"

Once the toll values are coded, the analyst must run this script to create five highway network files by time-of-day. In addition to being used for highway assignment, the five time-of-day highway networks are used as the background networks in developing the transit access connectors, and are also used in the transit skimming and assignment procedures. All of the five networks are identical except for the following:

1. The reversible lanes on the Golden Gate bridge are coded in the southbound direction in the Early AM, AM Peak, and Midday periods and the northbound direction in the PM Peak and Evening periods.
1. The Caldecott tunnel is coded with &lt;X&gt; lanes in the westbound direction in the Early AM, AM Peak Period, and Midday periods and &lt;X&gt; lanes in the eastbound direction in the PM Peak and Evening periods.
1. The fixed time toll delay links are given time-of-day specific values.
1. The shared ride toll bypass lanes are either left in place or deleted.

The analyst runs the script [CreateFiveHighwayNetworks.job](HighwayNetworkCoding#42-script-createfivehighwaynetworksjob) to create these five networks. In this script, a new variable called PNROK is created with a zero value for certain bridges. This variable is then used in a later script to prevent park-and-ride paths from being built across these bridges. Table 13 and Table 14 show the script settings and input and output network files.

*Table 13 Create Five Networks Script Input Link Attributes*

| Link Attribute Name | Description | Example |
|--|--|--|
| &lt;BRIDGENAME&gt;_BRIDGE_NOPNR | Disallows park-and-ride across certain bridges | benicia_bridge_nopnr |
| FFT | Sets the time-period-specific congested time equal to the free-flow time | CTIM = FFT |
| LANES | Sets the number of reversible lanes by time period on certain bridges | IF (a=7317 & b=7315 & time period=1) LANES = 2 |


*Table 14 Input and Output Files of CreateFiveHighwayNetworks.job*

| *Input/Output* | *Description* | *Example* |
|--|--|--|
| I | Highway Network with Toll values | withTolls.net |
| O | Highway Network by Time of Day | avgload&lt;timeperiod&gt;.net |
