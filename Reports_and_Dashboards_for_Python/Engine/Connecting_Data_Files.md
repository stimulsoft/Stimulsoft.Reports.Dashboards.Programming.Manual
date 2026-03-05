# Connecting Data Files

Typically, the connection parameters for data sources are stored in the report template itself. For working with file-based data sources such as XML, JSON, Excel, or CSV, don't required additional actions, as all algorithms are contained within the report generator script.

### Data loading event

To view and modify the connection parameters of file data before loading, you need to define the `onBeginProcessData` event for the component. In the event arguments will contain information about the connection to the file data source, including the connection name and type in the report template, as well as the path to the data file. A detailed description of the available property values â€‹â€‹passed in event arguments can be found in the [Report Engine Events](Events.md) section.


It is allowed to change the path to the data file. In this case, after the event completes, the report generator will request the file from the new path specified in the arguments. For example, if you need to change the path to the JSON data file for the specified connection:


**app.py**

from stimulsoft_reports.report import StiReportfrom stimulsoft_reports.events import StiDataEventArgs
def beginProcessData(args: StiDataEventArgs):if args.connection == 'MyJsonConnection':args->pathData = 'Data/Demo.json'

report = StiReport()report.onBeginProcessData += beginProcessDatareport.loadFile(url_for('static', filename='reports/SimpleList.mrt'))report.render()

If necessary, the same actions can be performed in a client-side JavaScript event:


**report.html**

```html

<script>
    function beginProcessData(args) {
        if (args.connection == "MyJsonConnection")
            args.pathData = "Data/Demo.json";
    }
</script>
```


> **Information**
>
> For an XML data source, the `onBeginProcessData` event will be triggered twice: first for reading the XSD schema, and second for reading the actual XML data file.

### Data processing event

To view and modify the connection parameters of file data before loading, you need to define the `onEndProcessData` event for the component. In the event arguments will include information about the connection to the file data source such as the connection name and type saved in the report template and the prepared `DataSet` object containing tables and rows of data retrieved from the file source. A detailed description of the available argument values can be found in the [Report Engine Events](Events.md) section.


**app.py**

from stimulsoft_reports.report import StiReportfrom stimulsoft_reports.events import StiDataEventArgs
def endProcessData(args: StiDataEventArgs):data = args.result.data

report = StiReport()report.onEndProcessData += endProcessDatareport.loadFile(url_for('static', filename='reports/SimpleList.mrt'))report.render()


If necessary, viewing or adjusting the loaded data can be done in a client-side JavaScript event. In the event arguments will include information about the connection to the file data source such as the connection name and type saved in the report template and prepared `DataSet` object containing tables and rows of data obtained from a file source. A detailed description of the available argument values can be found in the [Report Engine Events](Events.md) section.


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.onEndProcessData += 'endProcessData'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**report.html**

```html

<script>
    function endProcessData(args) {
        let dataSet = args.dataSet;
    }
</script>
```


> **Information**
>
> The report viewer and report designer components also have properties for the events mentioned above, which can be used to manage data loading in the manner described.

### Disabling file data adapter processing on the server-side

By default, file data loading is handled on the server side. This is necessary if you need to control connection parameters and the data itself in server-side events. However, if such control is not required, server-side file data processing can be disabled. In this case, data will be loaded using JavaScript, which slightly simplifies the event chain and speeds up data loading.


To disable file data adapters on the server side, simply set the `allowFileDataAdapters` property of the event handler to `False`, for example:


**index.php**

from stimulsoft_reports.report import StiReport
report = StiReport()report.handler.allowFileDataAdapters = False

### Using variables in the data file

It is possible to use variables in the form of expressions (as well as using expressions) when specifying the path to the file data source. A variable or expression is defined within curly braces. Multiple expressions can be used anywhere in the file path, for example:


**File Data Source**

```

https://localhost/data/{VariableJsonFileName}.json
https://localhost/data/json?id={VariableId}
https://localhost/{VariableCategory}/{VariableId}
```

So, a single data source can be transformed into REST syntax, eliminating the need to create multiple similar data sources to obtain uniform data. Combined with server-side Python logic and report generator events, this makes the data source even more flexible.

### Using OData

You can also use data retrieved from OData repositories for creating reports. In this case, authorization is required using a username, password, or token. The authorization parameters are specified in the connection string to the OData repository, using the ";" separator.


**report.html**

```html

<script>
    function beginProcessData(args) {
        let report = args.report;
        
        // Authorization using a user account
        let oDataDatabase = new Stimulsoft.Report.Dictionary.StiODataDatabase("OData", "OData", "https://services.odata.org/V4/Northwind/Northwind.svc;AddressBearer=adress;UserName=UserName;Password=Password;Client_Id=Your Client ID", false, null);
        
        // Authorization using a user token
        let oDataDatabase = new Stimulsoft.Report.Dictionary.StiODataDatabase("OData", "OData", "https://services.odata.org/V4/Northwind/Northwind.svc;Token=Enter your token", false, null);
        
        report.dictionary.databases.add(oDataDatabase);
        report.dictionary.synchronize();
        
        // Query with data filter
        var productsDataSource = report.dictionary.dataSources.getByName("Products");
        if (productsDataSource != null) productsDataSource.sqlCommand = "Products?filter=ProductID eq 2";
    }
</script>
```
