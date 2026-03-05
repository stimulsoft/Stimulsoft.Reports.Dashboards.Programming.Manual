# Designer Events

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To write interactive applications need to respond to changes in the application. The event system is used for this. It is represented in Stimulsoft Report Designer with the following events:


### onPrepareVariables

**Asynchronous event is called before filling in the variables in the report at the beginning of the report rendering. The event occurs immediately after execution onPrepareVariables event of the StiReport object. The event handler argument “event” is an object with the next fields:

                Name
              
              
                Description

                sender
              
              
                The identifier of the component, which initiated this event.

                event
              
              
                a string ID for the current event. By default, the value is set to PrepareVariables.

                report
              
              
                a report object StiReport.

                preventDefault
              
              
                a flag to prevent further processing of the event. By default, the value is set to false.

                async
              
              
                a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to false.

                designer.html

                ...
                designer.onPrepareVariables = (args, callback) => {
                args.variables[0].value = "Replace value";
                }
                ...**


### onBeginProcessData

**Asynchronous event is called before requesting the data for the report. The event occurs immediately after execution onBeginProcessData event of the StiReport object. The event handler argument “event” is an object with the next fields:

                Name
              
              
                Description

                sender
              
              
                The identifier of the component, which initiated this event.

                event
              
              
                a string ID for the current event. By default, the value is set to BeginProcessData.

                report
              
              
                a report object StiReport.

                preventDefault
              
              
                a flag to prevent further processing of the event. By default, the value is set to false.

                async
              
              
                a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to false.

                command
              
              
                a string ID for the current command. Can have values "TestConnection" and "ExecuteQuery" to call the command to test a connection and data acquisition respectively.

                database
              
              
                a string name of the current database.

                connection
              
              
                the name of the current connection to a data source, specified in report template.

                headers
              
              
                an array of the query headers.

                withCredentials
              
              
                an argument is used to provide the ability to set a cookies in the query.

                connectionString
              
              
                a connection string to the data source for a report.

                dataSource
              
              
                the name of the current data source, specified in the report template. It is set only for SQL data sources.

                queryString
              
              
                a string with the SQL query to the database for retrieving data. Used only with the command = "ExecuteQuery".

                timeout
              
              
                an argument is used to provide the ability to define the seconds of the query timeout.

                parameters
              
              
                a list of the query parameters.

                escapeQueryParameters
              
              
                a flag is used to provide the ability to use the escaped part of the request. By default, the value is set to true.

                pathData
              
              
                an argument is used to provide the ability to define a path to data file.

                tryParseDateTime
              
              
                a flag is trying to parse data as DateTime. 

                relationDirection
              
              
                an argument is used to provide the ability to change the direction of the relation between data sources.

                pathSchema
              
              
                an argument is used to provide the ability to define a path to XSD files.

                firstRowIsHeader
              
              
                a flag is used to provide the ability to use a first row as data header in Excel data source.

                collectionName
              
              
                a string collection name of the OData data source.

                separator
              
              
                a string separator of the CSV data source. 

                dataType
              
              
                an argument is used to provide the ability to set the data type of the GIS data source. 

                codePage
              
              
                an argument is used to provide the ability to set a code page of the CSV or DBF data source. 

                designer.html

                ...
                //Replace connection string
                designer.onBeginProcessData = (args) => {
                if (args.database == "MySQL")
                args.connectionString = "new connection string";
                }
                ...
                
                //Add a some data
                designer.onBeginProcessData = (args, callback) => {
                if (args.database == "MySQL"){
                args.preventDefault = true;
                var result = {
                success: true,
                rows: [
                ["value1", 1, false],
                ["value2", 1, true],
                ["value3", 2, false]
                ],
                columns: [
                "Column1_name",
                "Column2_name",
                "Column3_name"
                ],
                types:[
                "string",
                "int",
                "boolean"
                ]
                }
                
                // https://github.com/stimulsoft/DataAdapters.JS/
                callback(result);
                }
                }
                ...**


### onEndProcessData

**Is called after retrieving data for the report. The event occurs immediately after execution onEndProcessData event of the StiReport object. The event handler argument “event” is an object with the next fields:

                Name
              
              
                Description

                sender
              
              
                The identifier of the component, which initiated this event.

                event
              
              
                a string ID for the current event. By default, the value is set to EndProcessData.

                report
              
              
                a report object StiReport.

                command
              
              
                a string ID for the current command. Can have values "TestConnection" and "ExecuteQuery" to call the command to test a connection and data acquisition respectively.

                dataSource
              
              
                the name of the current data source, specified in the report template. It is set only for SQL data sources.

                connection
              
              
                the name of the current connection to a data source, specified in report template.

                database
              
              
                a string name of the current database.

                result
              
              
                a result dataset in a specific JSON format. It has two collections – columns and rows, with descriptions of columns and rows of data sources.

                designer.html

                ...
                designer.onEndProcessData = (args) => {
                if (args.command == "ExecuteQuery" && args.dataSource == "Categories")
                args.result.rows.push(rowData) ;
                // https://github.com/stimulsoft/DataAdapters.JS/
                }
                ...**


### onCreateReport

Asynchronous event Is called after a new report is created. The event handler argument “event” it is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **CreateReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. The default value is **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |
| isWizardUsed | The flag indicates that a new report is created with the help of the master (the `true` value) or a blank report is created (the `false` value). |


**designer.html**

```html
...
designer.onCreateReport = function (args) {
    var report = args.report;
       
    var database = new Stimulsoft.Report.Dictionary.StiJsonDatabase("DemoData", "http://localhost/Demo.json");
    report.dictionary.databases.add(database);
    report.dictionary.synchronize();
}
...
```


### onOpenReport

Asynchronous event is called before user click button for opening a report. The event handler argument event is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **OpenReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. The default value is **true**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |


**designer.html**

```html
...
//Call custom callback() function for loading template to designer
designer.onOpenReport = (args, callback) => {
    args.async = true;
    args.report = anotherReport;
    callback();
}
...
```


### onOpenedReport

Asynchronous event is called before user click button for opening a report before it is assigned to the designer. The event handler argument event is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **OpenedReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. The default value is **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |


**designer.html**

```html
...
//Add image to report resource when it has been opening
designer.onOpenedReport = (args, callback) => {
    args.async = true;
    var xhr = new XMLHttpRequest();
    xhr.open('GET', "Url to image");
    xhr.onload = function () {
        var imageData = xhr.response;
               
        var resource = new Stimulsoft.Report.Dictionary.StiResource("ImageName");
        resource.content = imageData;
        args.report.dictionary.resources.add(resource);
        callback();
    };
    xhr.send();
}
...
```


### onAssignedReport

The event is called after the report is assigned to the designer. The event handler argument event is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **AssignedReport**. |
| report | a report object **StiReport**. |


**designer.html**

```html
...
designer.onAssignedReport = (args) => {
    console.log("The report was assigned to the designer")
}
...
```


### onSaveReport

Asynchronous event is called before saving the report. The event handler argument event is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **SaveReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. The default value is **true**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |
| fileName | a saving file name. |
| autoSave | a flag is used to use autosave mode. The default value is **false**. |


**designer.html**

```html
...
//Remove report resources before saving
designer.onSaveReport = (args, callback) => {
    var report = args.report.clone();
    report.dictionary.resources.clear();
    args.report = report;
}
...
```


### onSaveAsReport

Asynchronous event is called before saving the report if user click **Save As** button. The event handler argument event is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **SaveAsReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. The default value is **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |
| fileName | a saving file name. |
| autoSave | a flag is used to use autosave mode. The default value is **false**. |


**designer.html**

```html
...
//Stop and redefinition the save method
designer.onSaveAsReport = (args, callback) => {
    args.preventDefault = true;
    var jsonString = args.report.saveToJsonString();
    // save report
}
...
```

### onPreviewReport

**Asynchronous event is called when going to the report preview tab. The event handler argument event is an object with the next fields:

                Name
              
              
                Description

                sender
              
              
                The identifier of the component, which initiated this event.

                event
              
              
                a string ID for the current event. By default it is PreviewReport.

                report
              
              
                a report object StiReport.

                preventDefault
              
              
                a flag to prevent further processing of the event. The default value is false.

                async
              
              
                a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to false.

                viewer
              
              
                a viewer object StiViewer.

                designer.html

                ...
                designer.onPreviewReport = function (args) {
                var dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
                dataSet.readJsonFile("Data/Demo.json");
                
                args.report.regData(dataSet.dataSetName, "", dataSet);
                }
                ...**


### onCloseReport

Asynchronous event is called after a report is closed, before the report has been unassigned from the report designer. The event handler argument “event” it is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **Close****Report**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. The default value is **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |


**designer.html**

```html
...
designer.onCloseReport = function (args) {
    console.log("The report was closed")
}
...
```

### onExit

**Is called before closing the designer. The event handler argument event is an object with the next fields:

                Name
              
              
                Description

                sender
              
              
                The identifier of the component, which initiated this event.

                event
              
              
                a string ID for the current event. By default it is Exit.

                designer.html

                ...
                designer.onExit = function (args) {
                console.log(args.event);
                }
                ...**
