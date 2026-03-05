# Viewer Events

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

In order to write interactive applications it is needed to respond to changes in the application. The event system which is represented in Stimulsoft Report Viewer can be used for this. The following events exist:


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

                viewer.html

                ...
                viewer.onPrepareVariables = (args, callback) => {
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

                viewer.html

                ...
                //Replace connection string
                viewer.onBeginProcessData = (args) => {
                if (args.database == "MySQL")
                args.connectionString = "new connection string";
                }
                ...
                
                //Add a some data
                viewer.onBeginProcessData = (args, callback) => {
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

                viewer.html

                ...
                viewer.onEndProcessData = (args) => {
                if (args.command == "ExecuteQuery" && args.dataSource == "Categories")
                args.result.rows.push(rowData) ;
                // https://github.com/stimulsoft/DataAdapters.JS/
                }
                ...**


### onPrintReport

Asynchronous event is called before printing the report. This is not relevant when viewing dashboards. The event handler argument “event” is an object with the next fields:


**Name
              
              
                Description

                sender
              
              
                The identifier of the component, which initiated this event.

                event
              
              
                a string ID for the current event. By default, the value is set to PrintReport.

                report
              
              
                a report for saving.

                preventDefault
              
              
                a flag to prevent further processing of the event. By default, the value is set to false.

                async
              
              
                a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to false.

                printAction
              
              
                a sting method name for printing.**


**viewer.html**

```html
...
//Remove image before report print
viewer.onPrintReport = (args) => {
    var page = args.report.renderedPages.getByIndex(0);
    var image = page.components.getByName("Image1");
    if (image)
        page.components.remove(image);
}
...
```


### onBeginExportReport

Asynchronous event is called before export but after applying the export options. The event handler argument “event” is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **BeginExportReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. By default, the value is set to **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |
| action | the action, which initiated export event - **StiExportAction**. |
| settings | export report settings. |
| format | export report format. Can have the following values: Stimulsoft.Report.StiExportFormat.Pdf, Stimulsoft.Report.StiExportFormat.Excel2007, Stimulsoft.Report.StiExportFormat.Word2007, Stimulsoft.Report.StiExportFormat.Html, Stimulsoft.Report.StiExportFormat.Html5, Stimulsoft.Report.StiExportFormat.Document. Stimulsoft.Report.StiExportFormat.Text, Stimulsoft.Report.StiExportFormat.Csv, Stimulsoft.Report.StiExportFormat.ImageSvg, Stimulsoft.Report.StiExportFormat.Ppt2007, Stimulsoft.Report.StiExportFormat.Odt, Stimulsoft.Report.StiExportFormat.Ods. |
| formatName | name of a selected report export format corresponds to the name of the constants in format list. |
| fileName | an exporting file name. |
| openAfterExport | The flag indicates that a report will be exported in a new browser tab (the `true` value) or after export completed file saving will be invoked (the `false` value). |


**viewer.html**

```html
...
viewer.onBeginExportReport = function (args) {
    switch (event.format) {
        case Stimulsoft.Report.StiExportFormat.Html:
        args.settings.zoom = 2;  // Set zoom to 200%
        break;
    }
    console.log("exporting");
}
...
```


### onEndExportReport

Asynchronous event is called after export report. The event handler argument “event” is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, it is set to **EndExportReport**. |
| fileName | an exporting file name. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. By default, the value is set to **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |
| action | the action, which initiated export event - **StiExportAction**. |
| format | export report format. Can have the following values: Stimulsoft.Report.StiExportFormat.Pdf, Stimulsoft.Report.StiExportFormat.Excel2007, Stimulsoft.Report.StiExportFormat.Word2007, Stimulsoft.Report.StiExportFormat.Html, Stimulsoft.Report.StiExportFormat.Html5, Stimulsoft.Report.StiExportFormat.Document. Stimulsoft.Report.StiExportFormat.Text, Stimulsoft.Report.StiExportFormat.Csv, Stimulsoft.Report.StiExportFormat.ImageSvg, Stimulsoft.Report.StiExportFormat.Ppt2007, Stimulsoft.Report.StiExportFormat.Odt, Stimulsoft.Report.StiExportFormat.Ods. |
| formatName | name of a selected report export format corresponds to the name of the constants in format list. |
| fileName | an exporting file name. |
| openAfterExport | The flag indicates that a report will be exported in a new browser tab (the `true` value) or after export completed file saving will be invoked (the `false` value). |
| data | export data to the string or byte array representation. |


**viewer.html**

```html
...
viewer.onEndExportReport = (args) => {
    args.fileName = "SampleFileName.txt";
}
...
```


### onInteraction

Asynchronous event is called while interactive action of the viewer (dynamic sorting, collapsing, drill-down, applying of parameters) until processing values by the report generator. The event handler argument “event” is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, it is set to **Interaction**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. By default, the value is set to **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |
| action | The identifier of the current interactive action can take the following values: - `Sorting` - This action happens when using sorting columns; - `DrillDown` - This action happens when using sorting columns; - `Collapsing` - This action happens when using of collapsing report blocks. |


**viewer.html**

```html
...
viewer.onInteraction = (args) => {
    if (args.action == "Variables")
        args.variables["Variable1"] = "New Value";
}
...
```


### onEmailReport

It is called before sending the report by email. This is not relevant when viewing dashboards. The event handler argument “event” is an object with the next fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event. By default, the value is set to **EmailReport**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |
| report | a report object **StiReport**. |
| settings | export email settings.: email - address of the recipient; subject - email subject; message - email message. |
| format | export report format. Can have the following values: Stimulsoft.Report.StiExportFormat.Pdf, Stimulsoft.Report.StiExportFormat.Excel2007, Stimulsoft.Report.StiExportFormat.Word2007, Stimulsoft.Report.StiExportFormat.Html, Stimulsoft.Report.StiExportFormat.Html5, Stimulsoft.Report.StiExportFormat.Document. Stimulsoft.Report.StiExportFormat.Text, Stimulsoft.Report.StiExportFormat.Csv, Stimulsoft.Report.StiExportFormat.ImageSvg, Stimulsoft.Report.StiExportFormat.Ppt2007, Stimulsoft.Report.StiExportFormat.Odt, Stimulsoft.Report.StiExportFormat.Ods. |
| formatName | name of a selected report export format corresponds to the name of the constants in format list. |
| fileName | an exporting file name. |
| data | export data to the string or byte array representation. |


**viewer.html**

```html
...
viewer.onEmailReport = (args, callback) => {
    args.async = true;
    
    var emailAddress = args.settings.email;
    var emailMessage = args.settings.message;
    var emailSubject = args.settings.subject;
    var emailAttachmentFileName = args.fileName;
    var emailAttachment = args.data;
    sendEmail(emailAddress, emailMessage, emailSubject, emailAttachmentFileName, emailAttachment);
    
    setTimeout(() => {
        callback();
    }, 5000);
}
...
```


### onDesignReport

It is called by pressing the Design button. The event handler argument “event” is an object with the following fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event, by default, it is set to **DesignReport**. |
| report | a report for designing. |


**viewer.html**

```html
...
var viewerOptions = new Stimulsoft.Viewer.StiViewerOptions();
viewerOptions.toolbar.showDesignButton = true;
var viewer = new Stimulsoft.Viewer.StiViewer(viewerOptions, "StiViewer", false);
viewer.renderHtml("content");

viewer.onDesignReport = (args) => {
    var viewerDiv = document.getElementById("content");
    viewerDiv.innerHTML = "";
    var designerOptions = new Stimulsoft.Designer.StiDesignerOptions();
    designerOptions.appearance.fullScreenMode = true;
    var designer = new Stimulsoft.Designer.StiDesigner(designerOptions, "StiDesigner", false);
    designer.renderHtml("content");
       
    designer.report = args.report;
}
...
```


### onShowReport

Asynchronous event is called after a report is rendered before its displaying in the viewer. The event handler argument “event” is an object with the following fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event, by default, it is set to **ShowReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. By default, the value is set to **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |


**viewer.html**

```html
...
viewer.onShowReport = function (args) {
    console.log("showing");
}
...
```

### onOpenReport

Asynchronous event that provides the ability to use custom method of opening templates. The event is called before the dialog box is opened and before report is assigned to the viewer. The event handler argument “event” is an object with the following fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event, by default, it is set to **OpenReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. By default, the value is set to **true**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |


**viewer.html**

```html
...
viewer.onOpenReport = (args) => {
    args.async = true;
    args.report = anotherReport;
    callback();
}
...
```


### onOpenedReport

Asynchronous event that provides the ability to change of the report before it is assigned to the viewer. The event is called after report has been opened and before report is assigned to the viewer. The event handler argument “event” is an object with the following fields:


| **Name** | **Description** |
| --- | --- |
| sender | The identifier of the component, which initiated this event. |
| event | a string ID for the current event, by default, it is set to **OpenedReport**. |
| report | a report object **StiReport**. |
| preventDefault | a flag to prevent further processing of the event. By default, the value is set to **false**. |
| async | a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to **false**. |


**viewer.html**

```html
...
viewer.onOpenedReport = (args) => {
    if (args.report.reportAuthor != "Stimulsoft") {
        args.preventDefault = true;
        window.alert("report.reportAuthor == " + args.report.reportAuthor);
    }
}
...
```
