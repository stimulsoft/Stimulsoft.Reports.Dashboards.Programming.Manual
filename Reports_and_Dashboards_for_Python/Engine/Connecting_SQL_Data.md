# Connecting SQL Data Adapters

To generate reports, the report generator allows using data from various SQL sources. Since pure JavaScript doesn’t have built-in methods for working with remote databases, this functionality is implemented using server-side Python code. To work with SQL data sources, no additional actions are required, all data adapters are already connected and configured for work.

### Data loading event

Working with SQL data sources does not require any additional actions; all data adapters are already connected and configured. If it is necessary to process parameters used for connecting to the data, the `onBeginProcessData` event of the report object is provided. This event can be triggered on either the client- or server-side. The event arguments will contain all necessary parameters for connecting to the SQL data source, as well as the SQL query parameters. Detailed descriptions of the available argument values can be found in the [Report Engine Events](Events.md) section.


An example of measuring a SQL query on the JavaScript client side, and a database connection string on the PHP server side:


**app.py**

```python

from stimulsoft_reports.events import StiDataEventArgs
from stimulsoft_reports.report import StiReport

def beginProcessData(args: StiDataEventArgs):
    if args.connection == 'MyConnectionName':
        args.connectionString = 'Server=localhost;Database=test;uid=root;password=******;'

report = StiReport()
report.onBeginProcessData += beginProcessData
report.onBeginProcessData += 'beginProcessData'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**report.html**

```html

<script>
    function beginProcessData(args) {
        if (args.dataSource == "MyDataSource")
            args.queryString = "SELECT * FROM ProductsTable";
    }
</script>
```

Thus, in the `onBeginProcessData` event, you can determine the database type, connection name, and data source name, as well as view and, if necessary, adjust the connection string and SQL query for data retrieval, and set the query parameter values. When modifying argument values on the server-side, the modified values will not be passed to the client-side, allowing the use of confidential data such as login and password in the connection string, table names, prefixes, etc.

**Data processing event**

To view or adjust the loaded data before registering and generating the report, the `onEndProcessData` event of the report object is provided. The event arguments will include all necessary connection parameters to the SQL data source, as well as the query result, containing column names, column types, and data rows retrieved from the SQL source. A detailed description of the available properties passed in event arguments can be found in the [Report Engine Events](Events.md) section.


**An example of the result of executing an SQL query, where the result already contains data prepared for the report:**


**app.py**

```python

from stimulsoft_reports.events import StiDataEventArgs
from stimulsoft_reports.report import StiReport

def endProcessData(args: StiDataEventArgs):
    args.result = {
        columns: ['id', 'username', 'phone'],
        types: ['int', 'string', 'string'],
        rows: [
            [1, 'Mario Pontes', '555-6874'],
            [2, 'Helen Bennett', '555-2376']
        ]
    }

report = StiReport()
report.onEndProcessData += endProcessData
report.onEndProcessData += 'endProcessData'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**report.html**

```html

<script>
    function endProcessData(args) {
        args.result = {
            columns: ["id", "username", "phone"],
            types: ["int", "string", "string"],
            rows: [
                [1, "Mario Pontes", "555-6874"],
                [2, "Helen Bennett", "555-2376"]
            ]
        };
    }
</script>
```

The available properties of the data object are listed in the table:


| **Name** | **Description** |
| --- | --- |
| `count` | The total number of columns in the SQL table of the data source. |
| `columns` | Column names of the SQL data source table. |
| `types` | Column types of the SQL data source table, converted to known types for the report generator. |
| `rows` | Data rows from the SQL data source, represented as an array of arrays of all table rows. |

All data from the SQL query execution result can be changed both on the JavaScript client side and on the PHP server side. The number of columns and data types must match to prevent incorrect interpretation of data by the report engine.


### Using parameters in an SQL query

If necessary, you can use parameters in an SQL query. To do this, add parameters to a special collection in the data source and set the required type and default value for each parameter. After that, the parameters can be used in the SQL query as follows:


**SQL Data Source**

```

SELECT * FROM @Parameter1 WHERE UserID = @Parameter2
```

All parameter values ​​are stored in the data source itself as a collection. The collection is an array of objects containing the parameter name, its type, and value. An example of the structure of the parameter array on the client's JavaScript side:


**app.py**

```python

args.parameters = [
   {
        name: "ParameterString",
        type: 752,
        typeName: "Text",
        value: "Text value"
  },
   {
        name: "ParameterInt",
        type: 3,
        typeName: "Int32",
     value: 20
   }
];
```


To access the request parameters, you can use the `onBeginProcessData` event, the parameter collection will be passed in the event arguments. It is allowed to change the values ​​of any parameters in the passed collection. An example of changing the value of the same parameter on the client JavaScript side and on the server PHP side:


**app.py**

from stimulsoft_reports.events import StiDataEventArgsfrom stimulsoft_reports.report import StiReport
def beginProcessData(args: StiDataEventArgs):if args.dataSource == 'DataSourceWithParams':args.parameters['Parameter1'].value = 'TableName'args.parameters['Parameter2'].value = 10

report = StiReport()report.onBeginProcessData += beginProcessDatareport.onBeginProcessData += 'beginProcessData'report.loadFile(url_for('static', filename='reports/SimpleListSQLParameters.mrt'))report.render()


**report.html**


<script>
function beginProcessData(args) {if (args.dataSource == "DataSourceWithParams") {args.parameters['Parameter1'].value = "TableName";args.parameters['Parameter2'].value = 10;}}
</script>

When modifying query parameter values, the type of the new value must match the type of the parameter being changed. Otherwise, executing the SQL query may return incorrect data or cause an internal execution error.


If the report uses multiple data sources, you must perform a check before assigning parameter values. Otherwise, a PHP script execution error may occur if any parameter is missing from the current data source.


> **Information**
>
> When modifying parameter values on the Python server side, the updated values will not be sent to the client side, so confidential data can safely be used as values.

### Using report variables as SQL parameters

It is possible to use a variable as an SQL parameter. To do this, set the property **Allow using as SQL parameter** in the report variable editor, after which it can be used in any SQL query. The syntax will be exactly the same as when using parameters in the data source.


> **Information**
>
> Such a variable will be included in the parameters collection only if it is used in the query. Parameters from the data source collection are always passed, even if they are not used in the query.

### Escaping parameter values

All parameter values will be automatically escaped to prevent SQL injections and ensure query execution security. If escaping is not required and you control the security of parameter values yourself, automatic escaping can be disabled. To do this, set the `escapeQueryParameters` property to `False` in the event handler:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.handler.escapeQueryParameters = False
```

After setting the specified property, using parameters becomes unsafe, and you must strictly control the values before executing SQL queries.


> **Information**
>
> Escaping applies only to SQL query parameters and variables used as parameters. If a variable is used as an expression, i.e., within curly braces, such as `{VariableName}`, escaping will not be applied in any case. A detailed description of how variables work can be found in the [Working with Report Variables](Using_Variables.md) section.


### Encrypting data sent to the client-side

If general data encryption is enabled using the encryptData option, all data sent to the client, including data from SQL sources, will be encrypted. This improves security but may slow down performance with large data volumes. There is an option to disable encryption specifically for SQL data sent to the client. To do this, simply set the encryptSqlData property of the event handler to False. After that, all data will be transmitted in plain JSON format. This should not significantly affect security, as only the data already displayed in the report will be sent in unencrypted form.


**app.py**

from stimulsoft_reports.report import StiReport
report = StiReport()report.handler.encryptSqlData = False
