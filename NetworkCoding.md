[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[NetworkCoding]]

***

For *Travel Model 1.5*, we will be using [NetworkWrangler](https://github.com/BayAreaMetro/NetworkWrangler) for network creation, pivoting from the [TM1_2015_Base_Network](https://github.com/BayAreaMetro/TM1_2015_Base_Network).

[Network building documentation](http://bayareametro.github.io/travel-model-two/netbuild/) in Travel Model Two's Documentation is therefore relevant, and supplemental TM1.5 information will be added here shortly.

## Roadway Project Examples

Roadway projects can take basically (one or more of) six actions:

| Action | Example Project |
|--------|-----------------|
| Create new nodes | No example project yet |
| Modify attributes for nodes | No example project yet |
| Delete nodes | None yet and this may not ever be necessary |
| Create new links | To be created |
| Modify attributes for links | Earthquake |
| Delete links | Earthquake|

More documentation to be filled in.

## Transit Project Examples

Transit projects are more complicated.  Some example actions:

| Action | Example Project |
|--------|-----------------|
| Adding a new line (including transfer links and funnel links) | CC_050025_EBart_to_Antioch |
| Removing a line | Earthquake (to be coded) |
| Rerouting a bus line | Earthquake (to be coded) |
| Extending an existing line |  SOL030002_FairfieldVacaville_Stn |

_**The following information/pages are old and likely need to be updated but are left here for reference.**_

---
This page describes the MTC highway and transit network coding, as well as procedures to check the result. It does so by walking through the steps to create final project level networks for a model application. The sections are:

## 1. [Highway network coding procedures and relevant scripts](HighwayNetworkCoding)

The MTC highway network is coded and maintained as a comprehensive highway network file, commonly referred to as the master highway network. The file consists of network links that represent the roadways. A project highway network file is developed in three stages from the master highway network file and consists of roadway links classified by functional class, zone connector links, and a few other additional links to support transit modeling.

## 2. [Transit network coding procedures and relevant scripts](TransitNetworkCoding)

The transit network consists of the following types of files: transit lines, access/egress/transfer links, and fares. The transit network is created from these files plus the transit background network that is created from the highway network.

## 3. [Transit network check procedures](TransitNetworkCheck)

Two network check scripts can be run to ensure the transit network is ready for use. The first check is to build the transit network to ensure the highway and transit networks are consistent (i.e. a node isnt missing in one file for example). The second check is to ensure the TP+ block files reference all the input files that make up the network.
