# Report Events

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

In order to write interactive applications it is needed to respond to changes in the application. The event system which is represented in **StiReport** object can be used for this. The following events exist:


### onPrepareVariables

**Asynchronous event is called before filling in the variables in the report at the beginning of the report rendering. The event handler argument “event” is an object with the next fields:

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
                report.onPrepareVariables = (args, callback) => {
                args.variables[0].value = "Replace value";
                }
                ...**


### onBeginProcessData

**Asynchronous event is called before requesting the data for the report. The event handler argument “event” is an object with the next fields:

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
                report.onBeginProcessData = (args) => {
                if (args.database == "MySQL")
                args.connectionString = "new connection string";
                }
                ...
                
                //Add a some data
                report.onBeginProcessData = (args, callback) => {
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

**Is called after retrieving data for the report. The event handler argument “event” is an object with the next fields:

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
                report.onEndProcessData = (args) => {
                if (args.command == "ExecuteQuery" && args.dataSource == "Categories")
                args.result.rows.push(rowData) ;
                // https://github.com/stimulsoft/DataAdapters.JS/
                }
                ...**

### onBeginRender

### Is called at the beginning of the report rendering. This is not relevant for the dashboards.


### onRendering

### Is called at the report is rendering when each report page is created. This is not relevant for the dashboards.


### onEndRender

### Is called at the ending of the report rendering. This is not relevant for the dashboards.


### onExportingRender

### Is called before a report export is started.


### onExportedRender

### Is called after a report export is ended.


### onPrinting

**Is called when report.print() or report.printToPdf() method is invoked. This is not relevant for the dashboards.

                viewer.html

                ...
                //Remove image before report printing
                report.onPrinting = () => {
                var page = report.renderedPages.getByIndex(0);
                var image = page.components.getByName("Image1");
                if (image)
                page.components.remove(image);
                }
                ...**


### onPrinted

**Asynchronous event is called when report.print() or report.printToPdf() method is invoked after a report is exported to Html or PDF file (depends on method type). This is not relevant for the dashboards. The event handler argument “event” is an object with the next fields:

                Name
              
              
                Description

                sender
              
              
                The identifier of the component, which initiated this event.

                event
              
              
                 string ID for the current event. By default, the value is set to Printed.

                report
              
              
                a report object StiReport.

                preventDefault
              
              
                a flag to prevent further processing of the event. By default, the value is set to false.

                async
              
              
                a flag is used to provide the ability to stop the execution of the event before the callback function is executed. By default, the value is set to false.

                data
              
              
                export data to the string or byte array representation.

                viewer.html

                ...
                //Stop to report print and define a custom print method
                report.onPrinted = (args) => {
                args.preventDefault = true;
                var printData = args.data;
                myPrintingMethod(printData);
                }
                ...**


### onRefreshing

**Is called after a report is rendered if report.refreshTime property is set more than zero. Also, this event is called when Refresh button is clicked in the viewer.**
