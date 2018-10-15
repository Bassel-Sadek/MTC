[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[UtilityExpressionCalculator]]

---

_(Special thanks to our friends at the [Maricopa Association of Governments](http://www.azmag.gov/) for their contribution to this section of the User's Guide)_

**Travel Model One** is largely a sequence of discrete choice models. The Coordinated Travel - Regional Activity Modeling Platform (CT-RAMP) upon which _Travel Model One_ is implemented uses the Utility Expression Calculator (UEC) Java package to both locate input variables and specify utility equations that describe each discrete choice. The input variables and specifications are defined and stored in a Microsoft Excel workbook. The use of Excel greatly enhances the flexibility and transparency of the model system -- utility coefficients, model structures, etc, can be edited via Excel (rather than via difficult to follow text files or source code).

## Methodology

Each UEC workbook (i.e. Excel file) consists of at least two worksheets. One must be the [[UECDataSheet]], which defines the input files used in the utility expressions, including zonal (vector) data and level-of-service "skims" (matrix data). The second, third, fourth, etc page specifies one or more multinomial or nested logit models via a unique [[UECUtilitySheet]]. The [[UECUtilitySheet]] consists of three sections, as follows:

1. The first section specifies the nesting structure of the logit model -- if omitted, a multinomial structure is assumed;
1. Next, variable names, or tokens, are defined for use in subsequent (moving down rows) utility equations; and,
1. The final section defines the utility terms, typically a variable and a coefficient for each of the logit model's alternatives.

The CT-RAMP Java code controls model flow, handles output files (e.g., trip tables, tour records), facilitates debugging, and allows for the UECs to access variables stored in memory (e.g., the results from upstream logit models).

The basic steps required to use the UEC Java package are to instantiate the UEC object and to then solve the UEC object -- the solve method returns an array of utilities. An example UEC instantiation is as follows:

`// create a UEC for an example mode choice model`

`String controlExcelFile = "ExampleModeChoice.xls"`

`int dataSheetIndex = 0;`

`int utilitySheetIndex = 1;`

`HashMap rbHashMap = !ResourceUtil.changeResourceBundleIntoHashMap(resourceBundle);`

`UtilityExpressionCalculator exampleUec = new !UtilityExpressionCalculator(new File(controlExcelFile), utilitySheetIndex, dataSheetIndex, rbHashMap,ExampleModeChoiceDMU;`

The UEC constructor call will read all of the data defined in the [[UECDataSheet]] into working memory and check the syntax on the [[UECUtilitySheet]] for consistency. Errors will cause the program to terminate; error details will be written to the log file. The last argument in the Utility Expression Calculator constructor is a reference to a decision-making unit (DMU) class. The DMU is the interface between the utility expressions specified in the [[UECUtilitySheet]] and variables expected to be stored in memory (i.e. because they were created from upstream model results or require complex calculations outside the easy functionality of the UEC). So-called DMU variables are specified in the UtilitySheet with the @ symbol. For example, "@autos" may refer to an automobile onwership market segment. Each @ variable specified in the UtilitySheet must have a corresponding getter method in the DMU class. To carry this example through, an @autos reference in the UtilitySheet of the !ExampleModeChoice.xls control file requires a public getAutos() method to be a part of the ExampleModeChoiceDMU class.

The resource bundle [Hash Map](http://docs.oracle.com/javase/6/docs/api/java/util/HashMap.html) must identify variables that are defined in the UEC DataSheet with the % symbol. For example, if the DataSheet references the property "%Project.Directory%", the resource bundle must include a string defining the variable "Project.Directory". (This is a typical implementation of a Java properties or resource bundle file). The above code example demonstrates how a resource bundle file can be translated into a Hash Map for use in the Utility Expression Calculator object.

To solve the UEC for a given decision making unit (which may be a zone pair, a traveler, or a group of travelers), the UEC solve method can be implemented as follows:

`// use the UEC class to compute logit model utilities`

`IndexValues indexValues = new !IndexValues();`

`indexValues.setOriginLocation(origin);`

`indexValues.setDestinationLocation(destination);`

`exampleModeChoiceDMU.setPersonDetails(person);`

`double[] exampleModeChoiceUtilities = exampleUec.solve(indexValues, exampleModeChoiceDMU, availFlag);`

In this example, the origin and destination of the traveler are being set in the Index Values object, which contains the index values used in the zone- and matrix-file indexing described in the UtilitySheet page. The person attributes are being set in the DMU object, which is an instance of the ExampleModeChoiceDMU class described above. The last argument is a boolean array (availFlag) which lets the solve method know which of the alternatives should be solved for; the availability flags can be used to speed up calculations but are not strictly necessary. The availability flag array is dimensioned by the number of alternatives and can be set to all true as a default.

The UEC solve method returs an array of doubles dimensioned to the number of alternatives specified in the UtilitySheet. The array contains the sumproduct of each of the formulas and coefficients for each alternative, which is the utility for each alternative. This array can then be used with a logit model object to first compute alternative probabilities and then simulate choices.

-- Main.DavidOry - 20 Dec 2011