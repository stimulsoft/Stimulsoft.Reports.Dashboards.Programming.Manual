# Connecting Data

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

Connection parameters to data sources are usually stored in the report template itself. But if necessary, you can use other ways to connect data.

**Data Sources from Files**

The **DataSet** object is used to store data. It has methods for loading data from various file formats. The **regData()** method is used to connect data in the report, in the arguments of which the prepared **DataSet** object is specified.

The data can be loaded from XML files using XSD schema.

**index.html**

```html
...
var dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
dataSet.readXmlSchemaFile("Demo.xsd");
dataSet.readXmlFile("Demo.xml");

var report = new Stimulsoft.Report.StiReport();
report.regData(dataSet.dataSetName, "", dataSet);
report.dictionary.synchronize();
...
```


And from JSON files:

**index.html**

```html
...
var dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
dataSet.readJsonFile("Demo.json");

var report = new Stimulsoft.Report.StiReport();
report.regData(dataSet.dataSetName, "", dataSet);
report.dictionary.synchronize();
...
```

Additional methods for loading data from files

The **DataSet** object has a wide range of methods for loading data:

readJsonFile(fileName) – loading a JSON file at the specified path;

readJson(string) – loading JSON data as a string;

readJson(data) – loading JSON data as a byte array;

readJson(obj) – using a JavaScript object as data;


readXmlFile(fileName) – loading an XML file at the specified path;

readXml(string) – loading XML data as a string;

readXml(data) – loading XML data as a byte array;

readXmlSchemaFile(fileName) – loading an XSD file at the specified path;

readXmlSchema(string) – loading XSD data as a string;

readXmlSchema(data) – loading XML data as a byte array;


> **Information**
>
> Loading data schema is optional. If you want to use a data schema, you should add it before loading the XML data.
