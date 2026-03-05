# Working with Data

As a rule, the connection parameters to data sources are stored directly within the report template — these can be either file-based data sources or SQL data sources. If it is necessary to connect data from code, a special method `regData()` is provided in the report object. The parameters for this method include the name of the data source in the report and the data itself. The data can be in JSON or XML format as a string, or as a PHP object or array.


Example of connecting data as an object:


**app.py**


from stimulsoft_reports.report import StiReport

report = StiReport()report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))

data = { "Customers": {

"CompanyName": "Chop-suey Chinese",

"Address": "Emilii Plater Street 49",

"Phone": 555123000,

"ContactTitle": "Sales Representative"}
}

report.regData("Demo", data)
report.render()

In some cases, it may be necessary to synchronize the report's data dictionary structure with the provided data. To do this, simply specify true as the third parameter of the `regData()` method. In this case, before building the report, the data dictionary will be synchronized.


**Information**


When using the Designer component, you can create a new report object and pass data to it with data dictionary synchronization enabled. In this case, the designer will open with a new report and data already prepared for use.

### Clearing connection parameters and the data dictionary

If the loaded report already has configured data connection parameters, they take precedence. If it is necessary to forcibly use your own data set, you can clear the connection parameters by calling the special `clearData()` method on the report object. By default, only the connection parameters themselves will be cleared. If you need to completely clear the data dictionary structure (removing all existing data sources), you must specify true as the method's parameter.


Example of connecting data after clearing the existing dictionary:


**app.py**


from stimulsoft_reports.report import StiReport

report = StiReport()report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.clearData(True)
data = '{"Customers": [{"CompanyName": "Centro comercial Moctezuma", "Address": "Sierras de Granada 9993", "Phone": 12355500, "ContactTitle": "Marketing Manager"}]}'
report.regData("Demo", data, True)report.render()

### Report preparation event

To connect data before generating the report or to modify the report itself, you can use the special `onBeforeRender` event of the report object. This event is triggered before the report is rendered, after it has been loaded. To connect data, simply call the `regReportData()` method from the event arguments. The parameters of this method are exactly the same as those of the `regData()` method of the report object.


Example of connecting data in a report event:


**app.py**


from stimulsoft_reports.report import StiReport

from stimulsoft_reports.events import StiReportEventArgs


def beforeRender(args: StiReportEventArgs):

data = '{"Customers": [{"CompanyName": "Centro comercial Moctezuma", "Address": "Sierras de Granada 9993", "Phone": 12355500, "ContactTitle": "Marketing Manager"}]}'

args.regReportData("Demo", data)


report = StiReport()report.onBeforeRender += beforeRenderreport.loadFile(url_for('static', filename='reports/SimpleList.mrt'))report.render()

**Information**


If data has already been assigned in the report using the `regData()` method of the report object, it will be overridden by the data specified in the event.


### Client-Side data connection

If needed, data can be connected using JavaScript functions of the report generator. For this, the `onBeforeRender` event of the report object can be used. The data can be loaded directly into a special `DataSet` object used for storing them. It provides functions for loading data from XML/XSD and JSON files. After the files are loaded, you must call the `regData()` method on the report object to register the data. The prepared `DataSet` object is passed as an argument to this function.


Example of loading data from an XML file using an XSD schema:


**app.py**


from stimulsoft_reports.report import StiReport

report = StiReport()report.onBeforeRender += 'beforeRender'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()


**report.html**


<script>

function beforeRender(args) {

let dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");


dataSet.readXmlSchemaFile("Demo.xsd");

dataSet.readXmlFile("Demo.xml");


//dataSet.readJsonFile("Demo.json");

let report = args.report;report.regData(dataSet.dataSetName, "", dataSet);report.dictionary.synchronize();}
</script>

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/How%20to%20Activate%20the%20Product.php).


Information


Loading a data schema is not required. However, if you want to use a data schema, it should be added before loading the XML data.

Example of loading data from a JSON file:


**app.py**


from stimulsoft_reports.report import StiReport

report = StiReport()report.onBeforeRender += 'beforeRender'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()


**report.html**


<script>

function beforeRender(args) {

let dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");

dataSet.readJsonFile("Demo.json");

let report = args.report;report.regData(dataSet.dataSetName, "", dataSet);report.dictionary.synchronize();}
</script>

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/How%20to%20Activate%20the%20Product.php).


In addition to the `readXmlFile()` and `readJsonFile()` functions, there are also `readXml()` and `readJson()` functions, which accept data in the form of a string or an object.


**Information**


The `report.dictionary.synchronize()` function is used to synchronize the connected data with the report template’s data dictionary. When this function is called, the report dictionary is created based on the structure of the data loaded into the DataSet. This function is not required if the dictionary has been created in advance and its structure matches the connected data.
