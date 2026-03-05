# Connecting SQL Data Adapters

The report generator allows the use of data from various SQL sources for building reports. Since pure JavaScript doesn’t have built-in methods for working with remote databases, this functionality is implemented through server-side PHP code. No additional actions are required to work with SQL data sources, as all data adapters are already connected and configured.

**Connection creation event**

If you need to control all possible parameters for connecting to a database, the `onDatabaseConnect` event is available. The event arguments will include all necessary parameters for connecting to the SQL data source, as well as the type and name of the database driver used. All connection parameters can be modified. Additionally, it’s possible to pass an already established database connection in the event arguments. A detailed description of the available property values passed in the event arguments can be found in the [Report Engine Events](Events.md) section.


Example of creating a connection to a MySQL database with a private SSL key:


**index.php**

```php

<?php
    use Stimulsoft\Events\StiConnectionEventArgs;
    use Stimulsoft\Report\StiReport;

    $report = new StiReport();
    $report->onDatabaseConnect = function (StiConnectionEventArgs $args)
    {
        $args->link = mysqli_init();
        mysqli_ssl_set($args->link, null, null, "./private/cert.pem", null, null);
        $args->link = mysqli_real_connect(
            $args->link, $args->info->host, $args->info->userId, $args->info->password,
            $args->info->database, $args->info->port, NULL, MYSQLI_CLIENT_SSL);
    };
    
    $report->render();
?>
```

**Data loading event**

If you need to process the parameters used for connecting to the database, the `onBeginProcessData` event is available. The event arguments will include all necessary parameters for connecting to the SQL data source, as well as the SQL query parameters. All connection parameters can be modified both on the client-side through JavaScript and on the server-side through PHP. A detailed description of the available property values passed in the event arguments is available in the [Report Engine Events](Events.md) section.


Example of modifying an SQL query on the JavaScript client-side and the database connection string on the PHP server-side:


**index.php**

```php
<?php
    use Stimulsoft\Events\StiDataEventArgs;
    use Stimulsoft\Report\StiReport;
    
    function beginProcessData(StiDataEventArgs $args) {
        if ($args->connection == 'MyConnectionName')
            $args->connectionString = 'Server=localhost;Database=test;uid=root;password=******;';
    };
    
    $report = new StiReport();
    $report->onBeginProcessData->append(beginProcessData);
    $report->onBeginProcessData->append('beginProcessData');
    $report->render();
?>

...

<script>
    function beginProcessData(args) {
        if (args.dataSource == "MyDataSource")
            args.queryString = "SELECT * FROM ProductsTable";
    }
</script>
```

The full example is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Using%20SQL%20Data%20Sources.php).


Thus, in the `onBeginProcessData` event, you can get the database type, connection name, and data source, as well as retrieve and, if necessary, modify the connection string and SQL query. If any property values are changed in the event arguments on the PHP server-side, the modified data will not be sent to the client. This allows the use of sensitive information such as login, password, table names, and prefixes.

**Data processing event**

The `onEndProcessData` event is provided for viewing or modifying the loaded data before registering it and generating the report. In the event arguments, connection parameters for the SQL data source are passed, as well as the result of the query execution, containing the column names, data types, and rows of data obtained from the SQL source. A detailed description of the available properties in the event arguments can be found in the [Report Engine Events](Events.md) section.


Here’s an example of the result of an executed SQL query, where the result already contains data prepared for the report:


**index.php**

```php

<?php
    use Stimulsoft\Events\StiDataEventArgs;
    use Stimulsoft\Report\StiReport;

    function endProcessData(StiDataEventArgs $args) {
        $args->result->columns = ['id', 'username', 'phone'];
        $args->result->types = ['int', 'string', 'string'];
        $args->result->rows = [
            [1, 'Mario Pontes', '555-6874'],
            [2, 'Helen Bennett', '555-2376']
        ];
    };

    $report = new StiReport();
    $report->onEndProcessData->append(endProcessData);
    $report->onEndProcessData->append('endProcessData');
    $report->render();
?>

...

<script>
    function endProcessData(args) {
        args.result.columns = ["id", "username", "phone"];
        args.result.types = ["int", "string", "string"];
        args.result.rows = [
            [1, "Mario Pontes", "555-6874"],
            [2, "Helen Bennett", "555-2376"]
        ];
    }
</script>
```

The available properties of the SQL query result object are in the table:


| **Name** | **Description** |
| --- | --- |
| `count` | Total number of columns in the SQL source table. |
| `columns` | Column names of the SQL source table. |
| `types` | Column types of the SQL source table, converted to recognized types for the report generator. |
| `rows` | Data rows from the SQL source table, represented as an array of arrays containing all rows from the table. |

All data in the SQL query result can be modified both on the client-side JavaScript and on the PHP server-side. The number of columns and data types must match to avoid incorrect data interpretation by the report generator.

**Using parameters in SQL queries**

SQL queries can use parameters. For this, parameters need to be added to a special collection in the data source, with each parameter assigned a type and a default value. These parameters can then be used in the SQL query, for example:


**SQL Data Source**

```

SELECT * FROM @Parameter1 WHERE UserID = @Parameter2
```

All parameter values are stored in the data source as a collection. The collection is an array of objects containing the parameter name, its type, and value. Here is an example of the parameter array structure on the client-side JavaScript:


**index.php**

```php

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

To access query parameters, you can use the `onBeginProcessData` event, where the parameter collection is passed in the event arguments. You are allowed to modify the values of any parameters in the collection. Here’s an example of changing the same parameter value on both the client-side JavaScript and PHP server-side:


**index.php**

```php

<?php
    use Stimulsoft\Events\StiDataEventArgs;
    use Stimulsoft\Report\StiReport;

    $report = new StiReport();
    $report->onBeginProcessData->append('
        args.parameters["Parameter1"] = "TableName";
    ');
    
    $report->onBeginProcessData->append(function (StiDataEventArgs $args) {
        $args->parameters['Parameter1']->value = 'TableName';
    });
    
    $report->render();
?>
```

When modifying query parameter values, the type of the new value must match the type of the parameter being changed. Otherwise, the execution of the SQL query may return incorrect data or trigger an internal execution error.


> **Information**
>
> When changing parameter values on the PHP server-side, the modified values will not be passed to the client-side, so confidential data can be used for these values.

If the report uses multiple data sources, you should check parameters before assigning them. Otherwise, a PHP script execution error may occur if a parameter is missing from the current data source. For example, if the report contains two data sources, both having one common parameter and the second data source having an additional unique parameter:


**index.php**

```php

$report->onBeginProcessData->append(function (StiDataEventArgs $args) {
    $args->parameters['Parameter1']->value = 'TableName';

    if ($args->dataSource == 'DataSource2')
        $args->parameters['Parameter2']->value = 10;
});
```

**Using a report variable as an SQL parameter**

It’s possible to use a variable as an SQL parameter. To do this, simply enable the **Allow using as SQL parameter** property in the report variable editor. Once this is done, the variable can be used in any SQL query. The syntax will be the same as when using parameters from a data source.


> **Information**
>
> Such a variable will only be passed in the parameter collection if it is used in the query. Parameters from the data source collection are always passed, even if they aren’t used in the query.

**Escaping parameter values**

All parameter values will be automatically escaped to prevent the possibility of SQL injections and to maintain query execution security. If escaping isn’t required, and you are managing parameter value security yourself, automatic escaping can be disabled. To do this, simply set the `escapeQueryParameters` property to `false` in the event handler:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->handler->escapeQueryParameters = false;
?>
```

Once this property is set, the use of parameters becomes unsafe, and you must strictly control the values before executing SQL queries.


> **Information**
>
> Escaping is applied only to SQL query parameters and variables used as parameters. If a variable is used as an expression, i.e., inside curly braces e.g., `{VariableName}`, escaping will not be applied in any case. A detailed description of working with variables can be found in the [Working with Report Variables](Using_Variables.md) section.


### Encrypting data transferred to the client-side

If global data encryption is enabled using the `$encryptData` option, all data transferred to the client, including data from SQL sources, will be encrypted. This enhances security but may slow down performance when handling large volumes of data. There is an option to disable encryption specifically for SQL data transferred to the client. To do this, simply set the `$encryptSqlData` property of the event handler to `false`. After this, all data will be transferred in plain JSON format. This should not significantly impact security, as only the data itself will be sent unencrypted, and this data is already displayed in the report in some form.


**index.php**

<?phpuse Stimulsoft\Report\StiReport;
$report = new StiReport();$report->handler->encryptSqlData = false;$report->process();?>
