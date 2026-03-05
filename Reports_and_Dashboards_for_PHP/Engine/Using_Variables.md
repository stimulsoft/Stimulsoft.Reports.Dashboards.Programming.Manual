# Work with Report Variables

The report generator allows you to use variables in expressions, queries, filters, and other report elements. You can preview and modify variable values from code before building the report.

### Access to values of variables from a code

The report generator provides an easy way to directly access variables in the report template through the data dictionary. To do this, you need to define the `onBeforeRender` event for the report object, in which the report object will be passed as an argument on the JavaScript client-side. A detailed description of the available properties passed in the event arguments can be found in the [Report Engine Events](Events.md) section.


To access a report variable, you should use the `getByName()` JavaScript function from the variable collection in the report’s data dictionary. To modify the value of a variable, simply assign a new value to the `value` property. There's no need to check the variable’s type as type conversion will be handled automatically.


Example of modifying a string and an integer value of selected variables on the JavaScript client- side:

**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onBeforeRender = 'beforeRender'; 
    $report->loadFile('reports/Variables.mrt');
    $report->render();
?>

<script>
    function beforeRender(args) {
        let report = args.report;
        
        let variableString = report.dictionary.variables.getByName("VariableString");
        variableString.value = "Text value";
        
        let variableInt = report.dictionary.variables.getByName("VariableInt");
        variableInt.value = "20";
    }
</script>
```

Direct access to variables in the report template on the PHP server-side isn’t supported.


> **Information**
>
> Variable values will be changed within the report template, and when the report is saved, the changes will be stored in the file. To modify variable values without altering the template, you can use the `onPrepareVariables` event, which is triggered when preparing the report's variable values before building the report.

### The event of preparing values of variables

The report generator allows easy access to variables before the report is built. To do this, define the `onPrepareVariables` event for the report object. The event arguments will contain a collection of report variables, including their types and values. If a variable is initialized as an expression, the calculated value of the expression will be passed into the collection. A detailed description of the available properties passed in the event arguments can be found in the [Report Engine Events](Events.md) section.


On the JavaScript client-side, the collection of variables is represented as an array of objects, each containing the variable's name, type, and value. It's permissible to change the values of variables, but the type of the new value must match the type of the variable being modified.


**index.php**

```php

<script>
    function prepareVariables(args) {      
        args.variables = [
            {
                name: "VariableString",
                type: "String",
                value: "Text value"
            },
            {
                name: "VariableInt",
                type: "Int32",
                value: 20
            }
    ]};
</script>
```

Example of modifying a variable on the JavaScript client-side:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onPrepareVariables = 'prepareVariables'; 
    $report->loadFile('reports/Variables.mrt');
    $report->render();
?>

...

<script>
    function prepareVariables(args) {
        let variables = args.variables;

        variables.find(item => item.name == "VariableString").value = "Text value";
        variables.find(item => item.name == "VariableInt").value = 20;
    }
</script>
```

On the PHP server-side, it's also possible to change the values of variables, ensuring that the new value matches the type of the variable being modified. Additionally, it is possible to create a new report variable if needed. The collection passed to the client will only contain variables whose values have been changed, as well as any newly created variables.


Example of modifying a variable on the PHP server-side:


**index.php**

```php

<?php
    use Stimulsoft\Events\StiVariablesEventArgs;
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onPrepareVariables = function (StiVariablesEventArgs $args) {
        $args->variables['VariableString']->value = 'Text value';
        $args->variables['VariableInt']->value = 20;
    };$report->loadFile('reports/Variables.mrt');
    $report->render();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Setting%20Report%20Variables%20on%20the%20Server-Side.php).


To modify the value of a simple variable, you just need to replace the value in the variable collection. The value must be of the same type as the original. Variables of the `DateTime` type are passed as string values in the format "YYYY-MM-dd HH-mm-ss".


**index.php**

```php

$args->variables['VariableString']->value = 'Value from Server-Side';
$args->variables['VariableInt']->value = 123;
$args->variables['VariableDecimal']->value = 123.456;
$args->variables['VariableDateTime']->value = '2021-03-20 22:00:00';
```

To modify a variable of the `Range` type, you need to use the nested `value->from` and `value->to` values of the selected variable in the collection. The format for each of these two values is the same as for a simple variable:


**index.php**

```php

$args->variables['VariableStringRange']->value->from = 'Aaa';
$args->variables['VariableStringRange']->value->to 
```

For modifying a variable of the `List` type, you can access the list value by its index. It’s also allowed to set the entire list at once using a prepared array:


**index.php**

```php

$args->variables['VariableStringList']->value[0] = 'Test';
$args->variables['VariableStringList']->value = ['1', '2', '2'];
```

To create a new variable not defined in the report, you need to assign a prepared associative array in the format `['value' => 'New Value']` to the variable collection, using the new variable name. After that, the variable can be used for report generation, though it will not be saved in the report template.


**handler.php**

```php

$args->variables['NewVariable'] = ['value' => 'New Value'];
```


> **Information**
>
> If a variable is used in an SQL query as an expression, written in curly braces like `{VariableName}`, its value will not be automatically escaped. You must ensure the security of the values yourself, or use the variable as a query parameter, for example `@VariableName`. Detailed information on parameter handling can be found in the [Connecting SQL Data Adapters](Connecting_SQL_Data.md) section.

### Report variables transferred in a URL query

The report generator has the ability to automatically assign values to variables passed in a URL request. To enable this, you need to set the `passQueryParametersToReport` property to true in the event handler:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();    
    $report->handler->passQueryParametersToReport = true;
    $report->process();
?>
```

All other actions will be handled automatically by the report generator. If the variable exists in the report, its value will be updated to the value from the URL request. If the variable doesn’t exist in the report, it will be created for the purpose of report generation, though the new variable will not be saved in the report template. Variable names passed in the URL request are case-insensitive.


> **Information**
>
> All variable values will be assigned before the `onPrepareVariables` event is triggered, so within this event, you can further control and adjust the assigned values if necessary.
