[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[ComputingEnvironment]]

***

# Computing Environment
The hardware and software MTC uses to execute _Travel Model One_ are described on this page. To date, MTC has not experimented enough with the model to define the minimum or ideal hardware configuration. As such, the description here is for a hardware set up that is sufficient. It is important to note that both the software and model structure are highly configurable and flexible; depending on the analysis needs, the required computing power could vary dramatically.

## Hardware

MTC uses a single server with the following characteristics:
* Operating system: Microsoft Windows Server 2012 R2 Standard, 64-bit;
* Processors: Two Intel Xeon E5-2680 v3 @ 2.50 GHz (24 cores, 48 logical processors);
* Memory (RAM): 256.0 GB

We have also successfully run the Travel Model on Amazon EC2 instances (m4.10xlarge) using custom images from Citilabs with Cube pre-installed.

## Software

The following software are required to execute the MTC travel model.
Paths are set in [SetPath.bat](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/runtime/SetPath.bat)

### Citilabs Cube Voyager
The travel model currently uses version 6.4.4 of [Citilabs](http://citilabs.com/) Cube software. The Cube software is used to build skims, manipulate networks, manipulate matrices, and perform assignments.

### Citilabs Cube Cluster
The Cube Cluster software allows for the Cube scripts to be multi-threaded. In the current approach, the travel model uses 48 computing nodes. However, the Cube scripts can be manipulated to use any number of computing nodes across any number of machines, provided each machine has, at a minimum, a Cube Voyager node license. Cube Cluster is not strictly necessary, as the Cube scripts can be modified to use only a single computing node. Such an approach would dramatically increase run times.

The COMMPATH environment variable for use with Cube Cluster is set in [SetPath.bat](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/runtime/SetPath.bat).

### Java and CT-RAMP

MTC's travel model operates on the open-source Coordinated Travel - Regional Activity-based Modeling Platform (or CT-RAMP) developed by [Parsons Brinckerhoff](http://pbworld.com/). The software is written in the [Java](http://java.com/en/) programming language. Because the CT-RAMP software compiles code "on-the-fly", the 64-bit Java Development Kit (version 1.8) must be installed on each computer running the CT-RAMP software. The Java Development Kit includes the Java Runtime Environment. The 64-bit version of the software allows CT-RAMP to take advantage of larger memory addresses.

### GAWK

Certain text file manipulations are handled in the travel model using the free [GAWK](http://www.gnu.org/software/gawk/) software. GAWK must be installed on the computer executing the Cube scripts.

### Microsoft Excel

The CT-RAMP software allows discrete choice models to be specified via so-called [UtilityExpressionCalculators](https://github.com/BayAreaMetro/travel-model-one/tree/master/model-files/model). These files are Excel-based.

### Python

[Python 2.7](https://www.python.org/)(64-bit) is used to execute a variety of utility scripts.  The following python modules are installed on MTC modeling servers:

```bat
E:\Model2D-Share\Projects>pip lis
Package         Version
--------------- ----------------
certifi         2019.11.28
chardet         3.0.4
DataExtract     8300.15.308.1149
dbfpy           2.3.1
idna            2.9
numpy           1.15.4+mkl
pandas          0.24.1
pip             10.0.1
PySAL           1.11.0
python-dateutil 2.8.0
pytz            2015.4
pywin32         224
requests        2.23.0
rpy2            2.7.4
Rtree           0.8.3
scipy           0.17.0
setuptools      16.0
Shapely         1.5.16
SimpleParse     2.2.0
singledispatch  3.4.0.3
six             1.9.0
TableauSDK      10200.17.328.755
urllib3         1.25.8
xlrd            0.9.3
XlsxWriter      0.7.7
xlutils         1.7.1
xlwt            1.0.0
```
Some of these packages are pulled in by other packages.  We have found it sufficient to install the following packages: Shapely, numpy, pandas, SimpleParse, xlrd, xlwt, xlutils, dbfpy, pywin32, and rpy2.

Please note that a variety of model utility scripts also use R and Tableau.

#### Tips for Setup
We typically run python from the Windows command line (See [How to Run a Python Script via a File or the Shell](https://www.pythoncentral.io/execute-python-script-file-shell/)).  We typically use 64-bit python 2.7

* In order to install the required python packages, we recommend downloading the versions compiled for Windows from [Christoph Gohlke's Unofficial Windows Binaries for Python Extension Packages](https://www.lfd.uci.edu/~gohlke/pythonlibs/).  These modules are downloadable as .whl files, which are installable using the [pip](https://pip.pypa.io/en/stable/installing/) command.  Note that you'll want to download the appropriate .whl file for your python installation. So if you're using 64-bit python 2.7, you'd want to install the .whl file that includes the string `cp27 `for python 2.7, and the string `win_amd64` for 64-bit.  You may need to [install the module as an administrator](https://www.howtogeek.com/194041/how-to-open-the-command-prompt-as-administrator-in-windows-8.1/).

* MTC modeling staff typically use the one of the SetupModel scripts (e.g. [SetUpModel_PBA50.bat](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/SetUpModel_PBA50.bat)) to copy required model inputs/code into place onto the modeling machines.  This is optional, but we find it helps us to reduce errors and to verify that the model run was setup correctly so we prefer it over manual copying/setup.
