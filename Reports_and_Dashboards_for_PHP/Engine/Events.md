# Engine Events

The report generator supports events that provide the ability to perform necessary operations before certain actions—both on the client-side JavaScript, including the Node.js platform, and on the PHP server-side.


To trigger an event on the client-side JavaScript, you need to add the name of the JavaScript function defined in the current HTML template to the event. If there’s no HTML template, or when generating or exporting a report on the server-side using the Node.js platform, instead of the function name, the event should be assigned the function itself as a string or lines of code. The event arguments will be passed in the function parameters or in a pre-defined args variable, which can be used in the event code.


To trigger an event on the PHP server-side, you need to add the PHP function itself, previously defined in the code, to the event. Assigning an anonymous PHP function to the event is also allowed. The event arguments will be passed in the function parameters.

You can add any number of functions, both client-side and server-side, to a single event. In this case, you need to use the special `append()` method instead of assigning a function, and pass the function as a parameter. The [event handler](PHP_Handler.md) will group the functions by type and execute them in the order they were added.


Here’s an example of different ways to add functions of various types to an event:


**index.php**

```php

<?php
    use Stimulsoft\Events\StiDataEventArgs;
    use Stimulsoft\Events\StiVariablesEventArgs;
    use Stimulsoft\Report\StiReport;
    
    function prepareVariables(StiVariablesEventArgs $args) {
        $variables = $args->variables;
    };
    
    $report = new StiReport();
    $report->onPrepareVariables->append(prepareVariables);
    $report->onPrepareVariables->append('prepareVariables');
    $report->onBeginProcessData = function(StiDataEventArgs $args) {
        $args->connectionString = 'Server=localhost;Database=test;uid=root;password=******;';
    };
    
    $report->onBeforeRender = 'args.report.dictionary.clear();'; 
    $report->onAfterRender = 'afterRender';
    
    $report->loadFile('reports/Variables.mrt');
    $report->render();
?>

...

<script>
    function prepareVariables(args) {
        let variables = args.variables;
    }
    
    function afterRender(args) {
        alert("The report rendering is completed.");
    }
</script>
```

Depending on the event, it can be triggered on both the client-side JavaScript and the PHP server-side simultaneously, or only on the client-side JavaScript, or only on the PHP server-side. This is due to the architecture of the components—the report generator uses a JavaScript core for building and exporting reports, which operates on the client-side, while server-side PHP code is used for data handling. These two components do not have direct access to each other, so events work separately, and data transfer is handled by the event handler. The description of each event will specify which type can be used. A detailed description of the event handler and usage examples can be found in the [Event Handler](PHP_Handler.md) section.


> **Infformation**
>
> All events that work on the client-side JavaScript also work on the Node.js server-side since the same JavaScript report core is used in that case.

The report generator supports the following events:

- [onDatabaseConnect](#ondatabaseconnect)
- [onBeforeRender](#onbeforerender)
- [onAfterRender](#onafterrender)
- [onBeginProcessData](#onbeginprocessdata)
- [onEndProcessData](#onendprocessdata)
- [onPrepareVariables](#onpreparevariables)


### onDatabaseConnect

[-] JavaScript  [+] PHP


The event is triggered before connecting to the database after all parameters have been received. A detailed description and usage examples can be found in the SQL Data Adapter Connections section. The table below lists the properties passed in the event arguments on the PHP server-side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event for this specific event has the value `StiEventType::DatabaseConnect` |
| `sender` | The component that initiated this event can have the following types: - `StiViewer` - `StiDesigner` |
| `database` | The database type can take one of the values from the `StiDatabaseType` enumeration. |
| `driver` | The name of the PHP database driver being used. |
| `info` | The database connection parameters obtained from the connection string. |
| `link` | The database connection ID. By default, it’s set to `null`. In this case, the connection will be created by the data adapter. |

### onBeforeRender

[+] JavaScript  [-] PHP


The event is triggered before the report is generated. A detailed description and usage examples can be found in the [Rendering Report](Rendering_Report.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event has the value `BeforeRender`. |
| `sender` | The component identifier that initiated this event can have the following values: - "`Report`" |
| `report` | The current report object. |


The table below lists the properties passed in the event arguments on the PHP server-side:


| **Наименование** | **Описание** |
| --- | --- |
| `event` | Идентификатор текущего события, для данного события имеет значение StiEventType::BeforeRender |
| `sender` | Компонент, который инициировал данное событие, может иметь следующие типы: ·    StiReport |
| `report` | Текущий объект отчета. |
| regReportData($name, $data, $synchronize = false) | Метод, позволяющий передать данные в отчет. В качестве аргументов может принимать следующие значения: $name – имя источника данных в отчете; $data – данные в виде XML либо JSON строки, либо в виде PHP объекта или массива; $synchronize – флаг, указывающий на необходимость синхронизации данных, по умолчанию false. |

### onAfterRender

[+] JavaScript  [-] PHP


The event is triggered after the report is generated. A detailed description and usage examples can be found in the [Rendering Report](Rendering_Report.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event has the value `AfterRender`. |
| `sender` | The component identifier that initiated this event can have the following values: - "`Report`" |
| `report` | The current report object. |

### onBeginProcessData

The event is triggered before requesting the data necessary for building the report. Detailed descriptions and usage examples can be found in the [Connecting Data Files](Connecting_Data_Files.md) and [Connecting SQL Data Adapters](Connecting_SQL_Data.md) sections.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event has the value "`BeginProcessData`". |
| `sender` | The component that initiated this event can have the following values: - `Report` - `Viewer` - `Designer` |
| `report` | Current report object |
| `command` | The identifier of the current command can have the following values: - `TestConnection` - a connection check is performed; - `ExecuteQuery` - data query is performed from the specified SQL source. - `GetSchema` - the XSD scheme is read from a file source. - `GetData` - data is read from a file source. |
| `connection` | The name of the current connection to a data source, specified in report template. |
| `database` | The name of the current database. It can take the following values: - `"XML"` - `"JSON"` - `"Excel"` - `"CSV"` - `"MySQL"` - `"MS SQL"` - `"PostgreSQL"` - `"Firebird"` - `"Oracle"` - `"ODBC"` |
| `dataSource` | The name of the current data source, specified in the report template. It is set only for SQL data sources. |
| `connectionString` | Connection string to the SQL data source. |
| `queryString` | The SQL query for getting data. It is used only with the `ExecuteQuery` command. |
| `pathData` | The path to the data source file, specified in the report template. It's set only for XML and JSON data sources. |
| `pathSchema` | The path to the data scheme file, specified in the report template. It is set only for XML data source. |
| `parameters` | The collection of parameters and their values, specified in an SQL data source. |
| `preventDefault` | This flag is an ability to stop further event processing by the report generator. The false value is set by default. |

In the table below, you can find the list of event handler arguments on the PHP server-side.


| **Name** | **Description** |
| --- | --- |
| event | The identifier of the current event for this specific event has the value `StiEventType::BeginProcessData`. |
| sender | The component that initiated this event can have the following types: - `StiReport` - `StiViewer` - `StiDesigner` |
| `command` | The identifier of the current command can have the following values: - `StiDataCommand::TestConnection` - a connection test is performed; - `StiDataCommand::RetrieveSchema` - a database schema request is executed for NoSQL data sources; - `StiDataCommand::ExecuteQuery` - a data query from the specified SQL source is executed; - `StiDataCommand::Execute` - a stored procedure is executed from the specified SQL source. |
| `connection` | The name of the current connection to a data source, specified in report template. |
| `database` | The name of the current database. It can take the following values: - `StiDatabaseType::MySQL` - `StiDatabaseType::MSSQL` - `StiDatabaseType::PostgreSQL` - `StiDatabaseType::Firebird` - `StiDatabaseType::Oracle` - `StiDatabaseType::MongoDB` - `StiDatabaseType::ODBC` |
| `dataSource` | The name of the current data source, specified in report template. |
| `connectionString` | Connection string to the SQL data source. |
| `queryString` | The SQL query for getting data. It is used only with the `StiDataCommand::ExecuteQuery` command. |
| `pathData` | Path to the data source file specified in the report template. This is set only for XML and JSON data sources. |
| `pathSchema` | Path to the data schema file specified in the report template. This is set only for XML data sources. |
| `parameters` | A collection of parameters and their values specified in the SQL data source. The parameter values are always passed in their original (unescaped) form. |

### onEndProcessData

The event is triggered after data is loaded but before the report is generated. Detailed descriptions and usage examples can be found in the [Connecting Data Files](Connecting_Data_Files.md) and [Connecting SQL Data Adapters](Connecting_SQL_Data.md) sections.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identificator of the current event has the "`EndProcessData`" value. |
| `sender` | The identificator of the component, which initialized this event can take the following values: - `Report` - `Viewer` - `Designer` |
| `report` | Current report object. |
| `command` | The identificator of the current command can take the following values: - `ExecuteQuery` - data is obtained from the specified SQL source. - `GetData` - data is obtained from a file source. |
| `connection` | The name of the current connection to a data source, specified in report table. |
| `database` | The name of the current database. It can take the following values: - `"XML"` - `"JSON"` - `"Excel"` - `"CSV"` - `"MySQL"` - `"MS SQL"` - `"PostgreSQL"` - `"Firebird"` - `"Oracle"` - `"ODBC"` |
| `dataSource` | The name of the current data source, specified in report template. It is set only for SQL data sources. |
| `dataSet` | The prepared Stimulsoft.System.Data.DataSet object contains tables and data rows, received from a file source. |
| `result` | The collection of columns, their types and data rows, received from an SQL source. |

In the table below, you can find the list of the event handler arguments on the PHP server-side.


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event for this specific event has the value StiEventType::EndProcessData. |
| `sender` | The identificator of the component, which initialized this event can take the following values: - `StiReport` - `StiViewer` - `StiDesigner` |
| `command` | The identifier of the current command can have the following values: - `StiDataCommand::TestConnection` - a connection test is performed; - `StiDataCommand::RetrieveSchema` - a database schema request is executed for NoSQL data sources; - `StiDataCommand::ExecuteQuery` - a data query from the specified SQL source is executed; - `StiDataCommand::Execute` - a stored procedure from the specified SQL source is executed. |
| `connection` | The name of the current connection to a data source, specified in report template. |
| `database` | The name of the current database. It can take the following values: - `StiDatabaseType::MySQL` - `StiDatabaseType::MSSQL` - `StiDatabaseType::PostgreSQL` - `StiDatabaseType::Firebird` - `StiDatabaseType::Oracle` - `StiDatabaseType::MongoDB` - `StiDatabaseType::ODBC` |
| `dataSource` | The name of the current data source, specified in report template. It is set only for SQL data sources. |
| `queryString` | The final SQL query with all parameters that was executed to retrieve data. Used only with the StiDataCommand::ExecuteQuery command. |
| `result` | Collection of columns and their types, as well as data rows retrieved from an SQL source, or string data obtained from a file source. |

### onPrepareVariables

The event is triggered before report generation after the report variables have been prepared. Detailed descriptions and usage examples can be found in the [Working with Report Variables](Using_Variables.md) section.


The table below lists the properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identificator of the current event has the "`PrepareVariables`" variable. |
| `sender` | The identificator of the component, which initialized this event can take the following values: - `Report` - `Viewer` - `Desig``ner` |
| `report` | Current report object. |
| `variables` | The collection of report variables and their values. |
| `preventDefault` | This flag gives an ability to stop the further event handler by the report generator. The `false` value is set by default. |

In the table below you can find the list of the event handler arguments on the PHP server-side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event for this specific event has the value `StiEventType::PrepareVariables`. |
| `sender` | The identificator of the component, which initialized this event can take the following values: - `StiReport` - `StiViewer` - `StiDesigner` |
| `variables` | The collection of report variables and their values. |
