[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[NetworkCoding]]

***

For *Travel Model 1.5*, we use [NetworkWrangler](https://github.com/BayAreaMetro/NetworkWrangler) for network creation, pivoting from the [TM1_2015_Base_Network](https://github.com/BayAreaMetro/TM1_2015_Base_Network).

## 0. [Network Building with NetworkWrangler](Network-Building-with-NetworkWrangler)

## 1. [Roadway Network Coding](HighwayNetworkCoding)

## 2. [Transit network Coding](TransitNetworkCoding)

## 3. [Transit network check procedures](TransitNetworkCheck)

Two network check scripts can be run to ensure the transit network is ready for use. The first check is to build the transit network to ensure the highway and transit networks are consistent (i.e. a node isnt missing in one file for example). The second check is to ensure the TP+ block files reference all the input files that make up the network.
