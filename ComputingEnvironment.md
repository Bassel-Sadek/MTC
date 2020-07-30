[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[ComputingEnvironment]]

***

# Computing Environment
The hardware and software MTC uses to execute _Travel Model One_ are described on this page. To date, MTC has not experimented enough with the model to define the minimum or ideal hardware configuration. As such, the description here is for a hardware set up that is sufficient. It is important to note that both the software and model structure are highly configurable and flexible; depending on the analysis needs, the required computing power could vary dramatically.

## Hardware

MTC uses a single server with the following characteristics:
* Operating system: Microsoft Windows Server 2012 R2 Standard, 64-bit;
* Processors: Two Intel Xeon E5-2680 v3 @ 2.50 GHz (24 cores, 48 logical processors);
* Memory (RAM): 256.0 GB

## Software

The following software are required to execute the MTC travel model.
Paths are set in [SetPath.bat](https://github.com/BayAreaMetro/travel-model-one/blob/master/model-files/runtime/SetPath.bat)

### Citilabs Cube Voyager
The travel model currently uses version 6.4.4 of [Citilabs](http://citilabs.com/) Cube software. The Cube software is used to build skims, manipulate networks, manipulate matrices, and perform assignments.

### Citilabs Cube Cluster
The Cube Cluster software allows for the Cube scripts to be multi-threaded. In the current approach, the travel model uses 48 computing nodes. However, the Cube scripts can be manipulated to use any number of computing nodes across any number of machines, provided each machine has, at a minimum, a Cube Voyager node license. Cube Cluster is not strictly necessary, as the Cube scripts can be modified to use only a single computing node. Such an approach would dramatically increase run times.

### Java and CT-RAMP

MTC's travel model operates on the open-source Coordinated Travel - Regional Activity-based Modeling Platform (or CT-RAMP) developed by [Parsons Brinckerhoff](http://pbworld.com/). The software is written in the [Java](http://java.com/en/) programming language. Because the CT-RAMP software compiles code "on-the-fly", the 64-bit Java Development Kit (version 1.8) must be installed on each computer running the CT-RAMP software. The Java Development Kit includes the Java Runtime Environment. The 64-bit version of the software allows CT-RAMP to take advantage of larger memory addresses.

### GAWK

Certain text file manipulations are handled in the travel model using the free [GAWK](http://www.gnu.org/software/gawk/) software. GAWK must be installed on the computer executing the Cube scripts.

### Microsoft Excel

The CT-RAMP software allows discrete choice models to be specified via so-called [UtilityExpressionCalculators](https://github.com/BayAreaMetro/travel-model-one/tree/master/model-files/model). These files are Excel-based.

### Python

[Python 2.7](https://www.python.org/) is used to execute a variety of utility functions. Please see the MTC GitHub repo [here](https://github.com/MetropolitanTransportationCommission/travel-model-one/blob/master/utilities/python-install/go_go_python.bat) for the Python packages used in Version 0.5 of the model.

Please note that a variety of model utility scripts also use R and Tableau.

#### Tips for Setup
We typically run python from the Windows command line (See [How to Run a Python Script via a File or the Shell](https://www.pythoncentral.io/execute-python-script-file-shell/)).  We typically use 64-bit python 2.7

* This involves setting your `PATH` environment variable so the command line knows where the python executable is located.  For example, if your `python.exe` is installed in `C:\Python27\`, then the command line will execute python when the `PATH` includes the path of the executable:

```bat
    C:\temp>set PATH=unset
    C:\temp>python
    'python' is not recognized as an internal or external command,
    operable program or batch file.

    C:\temp>set PATH=C:\Python27
    C:\temp>python
    Python 2.7.8 (default, Jun 30 2014, 16:08:48) [MSC v.1500 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>> quit()
```
* It also likely involves installing python packages, such as pandas, numpy, etc.  We recommend downloading the versions compiled for Windows from [Christoph Gohlke's Unofficial Windows Binaries for Python Extension Packages](https://www.lfd.uci.edu/~gohlke/pythonlibs/).  These modules are downloadable as .whl files, which are installable using the [pip](https://pip.pypa.io/en/stable/installing/) command.  Note that you'll want to download the appropriate .whl file for your python installation. So if you're using 64-bit python 2.7, you'd want to install the .whl file that includes the string `cp27 `for python 2.7, and the string `win_amd64` for 64-bit.  You may need to [install the module as an administrator](https://www.howtogeek.com/194041/how-to-open-the-command-prompt-as-administrator-in-windows-8.1/).
