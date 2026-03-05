# Report Engine Events

The report generator supports events that allow you to perform custom operations before specific actions—both on the JavaScript client side, including the Node.js platform and on the Python server side.


To trigger an event on the JavaScript client side, you need to assign the name of a JavaScript function defined in the HTML template as a string to the event handler. If no HTML template is used—such as when building or exporting a report on the server using the Node.js platform—then instead of the function name, you must assign the actual function code as a string or lines of code to the event. The event arguments will be available in a predefined variable called `args`, which can be used within the function.

To trigger an event on the Python server side, you must assign a previously defined Python function to the event. The event arguments will be passed as parameters to that function.
Any number of functions, both client and server, can be added to a single event. An example of different options for adding functions of different types to an event:


**app.py**

```python

def prepareVariables(args: StiVariablesEventArgs):
    variables = args.variables

report = StiReport()
report.onPrepareVariables += prepareVariables
report.onPrepareVariables += 'prepareVariables'
report.onBeforeRender += 'args.report.dictionary.clear();'
report.onAfterRender += 'afterRender'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**report.html**

```html

<script>
    function prepareVariables(args) {
        let variables = args.variables;
    }

    function afterRender(args) {
        alert("The report rendering is completed.");
    }
</script>
```

Depending on the specific event, it may be triggered on both the JavaScript client and the Python server simultaneously, or only on the JavaScript client, or only on the Python server. This is due to the component architecture: the JavaScript report engine (used for building and exporting reports) runs on the client side, while the Python code is responsible for data processing on the server. These two parts do not have direct access to each other, so events work independently, and data exchange is handled by the event handler. Each event description specifies which types of functions can be used. A detailed explanation of the event handler and usage examples can be found in the [Event Handler](Handler.md) section.


> **Information**
>
> All events that work on the JavaScript client side also function on the Node.js server side, since the same JavaScript report engine is used in both cases.

Some event arguments accept values from enumerations, which are defined in specific namespaces. All enumerations used in report generator events are listed in the code block below:


**app.py**

```python

from stimulsoft_reports.enums import StiDataCommand, StiDatabaseType, StiEventType
```

The report generator supports the following events:


- [onDatabaseConnect](#ondatabaseconnect)
- [onBeforeRender](#onbeforerender)
- [onAfterRender](#onafterrender)
- [onBeginProcessData](#onbeginprocessdata)
- [onEndProcessData](#onendprocessdata)
- [onPrepareVariables](#onpreparevariables)

### onDatabaseConnect

[-] JavaScript  [+] Python


The event is called before connecting to the database after all parameters have been received. A detailed description and usage examples can be found in the [Connecting SQL Data Adapters](Connecting_SQL_Data.md) section. The table below lists the properties passed in the event arguments on the Python server side:


| **Name** | **Description** |
| --- | --- |
| event | The identifier of the current event, for this event the value is `StiEventType.DATABASE_CONNECT` |
| sender | The component that triggered this event can have the following types: ·    `StiViewer` ·    `StiDesigner` |
| database | Database type, can take one of the values ​​of the `StiDatabaseType` enumeration. |
| driver | The name of the Python database driver used. |
| info | Database connection parameters obtained from the connection string. |
| link | The identifier of the database connection. The default value is None, in which case the connection will be created by the data adapter. |


### onBeforeRender

[+] JavaScript  [+] Python


The event is called after the report is built. A detailed description and usage examples are in the [Report Rendering](Rendering_Report.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value  "`BeforeRender`". |
| `sender` | Identifier of the component that initiated this event, which can have the following values: - `"Report"` - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |

The table below lists the properties passed in event arguments on the Python server-side:


| **Name** | **Description** |
| --- | --- |
| event | Current event identifier, for this event the value is `StiEventType.BEFORE_RENDER` |
| sender | The component that triggered this event can have the following types: ·    `StiReport` |
| report | Current report object. |
| regReportData(name, data, synchronize = False) | A method that allows you to pass data to a report. It can take the following values ​​as arguments: `name` – the name of the data source in the report; `data` – data in the form of an XML or JSON string, or in the form of a Python object or dictionary; `synchronize` – a flag indicating the need to synchronize data, `False` by default. |

### onAfterRender

[+] JavaScript  [-] Python


The event is called after the report is built. A detailed description and usage examples are in the [Report Rendering](Rendering_Report.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value  "`AfterRender`". |
| `sender` | Identifier of the component that initiated this event, which can have the following values: - `"Report"` - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |


### onBeginProcessData

[+] JavaScript  [+] Python


The event is called after loading data before building a report. A detailed description and examples of use are in the [Connecting Data Files](Connecting_Data_Files.md) and [Connecting SQL Data Adapters](Connecting_SQL_Data.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value  "`BeginProcessData`". |
| `sender` | Identifier of the component that initiated this event, which can have the following values: - `"Report"` - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `command` | Identifier of the current command, which can have the following values: - `"TestConnection"` - checks the connection; - `"ExecuteQuery"` - queries data from the specified SQL source; - `"GetSchema"` - reads the XSD schema from the file source; - `"GetData"` - reads data from the file source. |
| `connection` | Name of the current data source connection specified in the report template. |
| `database` | Name of the current database, which can have the following values: - `"XML"` - `"JSON"` - `"Excel"` - `"CSV"` - `"MySQL"` - `"MS SQL"` - `"PostgreSQL"` - `"Firebird"` - `"Oracle"` - `"MongoDB"` - `"ODBC"` |
| `dataSource` | Name of the current data source specified in the report template. Set only for SQL data sources. |
| `connectionString` | Connection string to the SQL data source. |
| `queryString` | SQL query for data retrieval. Used only with the  `ExecuteQuery` command. |
| `pathData` | Path to the data source file specified in the report template. Set only for XML and JSON data sources. |
| `pathSchema` | Path to the data schema file specified in the report template. Set only for the XML data source. |
| `parameters` | Collection of parameters and their values specified in the SQL data source. |
| `preventDefault` | This flag allows stopping further event processing by the report generator. The default value is  `false`. |

The table below lists the properties passed in event arguments on the Python server-side:


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value  `StiEventType.BEGIN_PROCESS_DATA`for this event. |
| `sender` | Identifier of the component that initiated this event, which can have the following values: - `StiHandler` - `StiReport` - `StiViewer` - `StiDesigner` |
| `command` | Identifier of the current command, which can have the following values: - `StiDataCommand.TEST_CONNECTION` - checks the connection; - `StiDataCommand.RETRIEVE_SCHEMA` - queries the database schema for NoSQL data sources; - `StiDataCommand.EXECUTE_QUERY` - queries data from the specified SQL or NoSQL source; - `StiDataCommand.EXECUTE` - executes a stored procedure from the specified SQL source. |
| `connection` | Name of the current data source connection specified in the report template. |
| `database` | Name of the current database, which can have the following values: - `StiDatabaseType.XML` ·    `StiDatabaseType.JSON` ·    `StiDatabaseType.CSV` - `StiDatabaseType.MYSQL` - `StiDatabaseType.MSSQL` - `StiDatabaseType.POSTGRESQL` - `StiDatabaseType.FIREBIRD` - `StiDatabaseType.ORACLE` - `StiDatabaseType.MONGODB` - `StiDatabaseType.ODBC` |
| `dataSource` | Name of the current data source specified in the report template. |
| `connectionString` | Connection string to the SQL data source. |
| `queryString` | SQL query for data retrieval. Used only with the `StiDataCommand.EXECUTE_QUERY`command. |
| `pathData` | Path to the data source file specified in the report template. |
| `pathSchema` | Path to the data schema file specified in the report template. Set only for XML data source. |
| `parameters` | Collection of parameters and their values specified in the SQL data source. Values are always passed in their original (unescaped) form |

### onEndProcessData

[+] JavaScript  [+] Python


The event is called after loading data before building a report. A detailed description and examples of use are in the [Connecting Data Files](Connecting_Data_Files.md) and [Connecting SQL Data Adapters](Connecting_SQL_Data.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value  "`EndProcessData`" |
| `sender` | Identifier of the component that initiated this event, which can have the following values - `"Report"` - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `command` | Identifier of the current command, which can have the following values: - `"ExecuteQuery"` - data retrieved from the specified SQL source. - `"GetData"` - data retrieved from the file source |
| `database` | Name of the current database, which can have the following values:: - `"XML"` - `"JSON"` - `"Excel"` - `"CSV"` - `"MySQL"` - `"MS SQL"` - `"PostgreSQL"` - `"Firebird"` - `"Oracle"` - `"MongoDB"` - `"ODBC"` |
| `connection` | Name of the current data source connection specified in the report template. |
| `dataSource` | Name of the current data source specified in the report template. Set only for SQL data sources. |
| `dataSet` | The prepared `Stimulsoft.System.Data.DataSet`, object containing tables and data rows from the file source. |
| `result` | A collection of columns and their types, along with data rows retrieved from the SQL source. |

The table below lists the properties passed in event arguments on the Python server side:


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value  `StiEventType.END_PROCESS_DATA`for this event. |
| `sender` | Identifier of the component that initiated this event, which can have the following values: - `StiHandler` - `StiReport` - `StiViewer` - `StiDesigner` |
| `command` | Identifier of the current command, which can have the following values: - `StiDataCommand.TEST_CONNECTION` - checks the connection; - `StiDataCommand.RETRIEVE_SCHEMA` - requests the database schema for NoSQL data sources; - `StiDataCommand.EXECUTE_QUERY` - queries data from the specified SQL or NoSQL source; - `StiDataCommand.EXECUTE` - executes a stored procedure from the specified SQL source. |
| `connection` | Name of the current data source connection specified in the report template. |
| `database` | Name of the current database, which can have the following values: - `StiDatabaseType.XML` ·    `StiDatabaseType.JSON` ·    `StiDatabaseType.CSV` - `StiDatabaseType.MYSQL` - `StiDatabaseType.MSSQL` - `StiDatabaseType.POSTGRESQL` - `StiDatabaseType.FIREBIRD` - `StiDatabaseType.ORACLE` - `StiDatabaseType.MONGODB` - `StiDatabaseType.ODBC` |
| `dataSource` | Name of the current data source specified in the report template. Set only for SQL data sources. |
| `queryString` | The final SQL query with all parameters used for data retrieval. Used only with the StiDataCommand.EXECUTE_QUERY command. |
| `result` | A collection of columns and their types, along with data rows retrieved from the SQL or NoSQL source. |

### onPrepareVariables

[+] JavaScript  [+] Python


The event is called before the report is built after the report variables have been prepared. A detailed description and usage examples are in the [Working with Report Variables](Using_Variables.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value  "`PrepareVariables`". |
| `sender` | Identifier of the component that initiated this event, which can have the following values: - `"Report"` - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `variables` | Collection of report variables and their values. |
| `preventDefault` | This flag allows stopping further event processing by the report generator. The default value is `false`. |

The table below lists the properties passed in event arguments on the Python server side:


| **Name** | **Description** |
| --- | --- |
| `event` | Identifier of the current event, with the value `StiEventType.PREPARE_VARIABLES`for this event. |
| `sender` | Identifier of the component that initiated this event, which can have the following values: - `StiHandler` - `StiReport` - `StiViewer` - `StiDesigner` |
| `variables` | Collection of report variables and their values |
