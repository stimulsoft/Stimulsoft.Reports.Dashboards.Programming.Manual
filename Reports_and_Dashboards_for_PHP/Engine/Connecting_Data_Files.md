# Connecting Data Files

Typically, data source connection parameters are stored within the report template. For working with file data sources such as XML, JSON and CSV, no additional actions are required as all the necessary algorithms are included in the report generator script.


### Data loading event

To view and modify file data connection parameters before loading, you need to define the `onBeginProcessData` event for the component. The event arguments will include information about the connection to the file data source, specifically, the connection name and type in the report template, as well as the path to the data file. A detailed description of the available property values transmitted in the event arguments can be found in the [Report Engine Events](Events.md) section.


You are allowed to change the path to the data file. In this case, after the event completes, the report generator will request the file from the new path specified in the arguments. For example, if you need to change the path to the JSON data file for the specified connection:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Events\StiDataEventArgs;

    $report = new StiReport();
    $report->onBeginProcessData = function (StiDataEventArgs $args) {
        if ($args->connection == "MyJsonConnection")
            $args->pathData = "Data/Demo.json";
    };
    
    $report->render();
    $report->process();
?>
```

If needed, the same actions can be performed within a JavaScript client-side event:


**index.php**

<?phpuse Stimulsoft\Report\StiReport;
$report = new StiReport();$report->onBeginProcessData = 'beginProcessData';$report->render();?>
function onBeginProcessData(args) {if (args.connection == "MyJsonConnection")args.pathData = "Data/Demo.json";}


> **Information**
>
> The `onBeginProcessData` event will be invoked twice for an XML data source: first time to read an XSD scheme, second time to read an XML data file.

**Data Processing Event**

To view or modify the loaded data before connecting it and generating the report, you need to define the `onEndProcessData` event for the component. The event arguments will include information about the connection to the file-based data source—such as the connection name and type stored in the report template—as well as the data loading result, which contains the loaded data as a string. A detailed description of the available property values passed in the event arguments can be found in the [Report Engine Event](Events.md) section.


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Events\StiDataEventArgs;

    $report = new StiReport();
    $report->onEndProcessData = function (StiDataEventArgs $args) {
        $data = $args->result->data;
    };
    
    $report->render();
    $report->process();
?>
```

If necessary, you can view or modify the loaded data within the JavaScript client-side event. In the event arguments, information about the file data source connection will be passed, including the connection name and type saved in the report template, as well as the prepared `DataSet` object containing the tables and rows of data obtained from the file source. A detailed description of the available property values passed in the event arguments is available in the [Report Engine Event](Events.md) section.

**index.php**

<?phpuse Stimulsoft\Report\StiReport;
$report = new StiReport();$report->onEndProcessData = 'onEndProcessData';$report->renderHtml();?>
function onEndProcessData(args) {let dataSet = args.dataSet;}

### Disabling server-side processing of file data adapters

By default, file data loading is performed on the server side. This is useful when you need to control connection parameters and the data itself within server-side events. However, if this is not required, server-side processing of file data can be disabled. In this case, data loading will be handled via JavaScript, which simplifies the event chain and speeds up data retrieval.


To disable file data adapters on the server side, simply set the `$allowFileDataAdapters` property of the event handler to `false`, for example:


**index.php**

<?phpuse Stimulsoft\Report\StiReport;
$report = new StiReport();$report->handler->allowFileDataAdapters = false;?>

**Using variables in file data**

It is possible to use variables or expressions when specifying the path to the file data source. Variables or expressions are defined in curly braces. You can use multiple expressions anywhere in the data file path, for example:


**File Data Source**

```

https://localhost/data/{VariableJsonFileName}.json
https://localhost/data/json.php?id={VariableId}
https://localhost/{VariableCategory}/{VariableId}
```

This way, one data source can be transformed into REST syntax, eliminating the need to create multiple similar data sources for retrieving similar data. Combined with server-side PHP logic and report generator events, this can make the data source even more flexible.

**Using Odata**

You can also use data from OData stores to create reports. In this case, you must perform authentication using a username, password, or token. The authentication parameters are specified in the OData connection string, separated by a ";" delimiter.


**index.php**

```php

// Authorization using a user account
var oDataDatabase = new Stimulsoft.Report.Dictionary.StiODataDatabase("OData", "OData", "https://services.odata.org/V4/Northwind/Northwind.svc;AddressBearer=adress;UserName=UserName;Password=Password;Client_Id=Your Client ID", false, null);

// Authorization using a user token
var oDataDatabase = new Stimulsoft.Report.Dictionary.StiODataDatabase("OData", "OData", "https://services.odata.org/V4/Northwind/Northwind.svc;Token=Enter your token", false, null);

report.dictionary.databases.add(oDataDatabase);
report.dictionary.synchronize();

// Query with data filter
var productsDataSource = report.dictionary.dataSources.getByName("Products");
if (productsDataSource != null) productsDataSource.sqlCommand = "Products?$filter=ProductID eq 2";
```
