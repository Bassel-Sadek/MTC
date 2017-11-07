[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[NetworkCoding]]

***

This page describes the MTC highway and transit network coding, as well as procedures to check the result. It does so by walking through the steps to create final project level networks for a model application. The sections are:

## 1. [Highway network coding procedures and relevant scripts](HighwayNetworkCoding)

The MTC highway network is coded and maintained as a comprehensive highway network file, commonly referred to as the master highway network. The file consists of network links that represent the roadways. A project highway network file is developed in three stages from the master highway network file and consists of roadway links classified by functional class, zone connector links, and a few other additional links to support transit modeling.

## 2. [Transit network coding procedures and relevant scripts](TransitNetworkCoding)

The transit network consists of the following types of files: transit lines, access/egress/transfer links, and fares. The transit network is created from these files plus the transit background network that is created from the highway network.

## 3. [Transit network check procedures](TransitNetworkCheck)

Two network check scripts can be run to ensure the transit network is ready for use. The first check is to build the transit network to ensure the highway and transit networks are consistent (i.e. a node isnt missing in one file for example). The second check is to ensure the TP+ block files reference all the input files that make up the network.
