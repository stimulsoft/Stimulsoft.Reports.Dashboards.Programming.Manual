# PHP Events Handler

The report generator, as well as the report viewer and designer, can trigger client-side events, send them to the PHP server for further processing, and receive the prepared response. All actions are implemented in the event handler, so there is no need to use any additional functions to establish communication between the client and server or to transfer data. To work with a selected event, you simply need to add the function name to the handler, and the specified function will automatically be triggered when the selected event occurs. Events can be triggered both on the client-side on JavaScript and on the server-side on PHP. If needed, multiple functions of any type can be added to the same event.

### Triggering JavaScript events on the client-side

To trigger a JavaScript event, you need to add the function name as a string to the handler. All necessary data will be passed in the event arguments. A list of available properties passed in the arguments for all events can be found in the [Report Engine Events](Events.md) section. Here's an example of displaying a message with the number of pages in the generated document after the report is built:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onAfterRender = 'afterRender'; 
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
?>

...

<script>
    function afterRender(args) {
        let pagesCount = args.report.renderedPages.count;
        alert("The report is rendered, pages: " + pagesCount);
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


In this example, you can retrieve the JavaScript report object from the event arguments and read the number of pages built in the document.


> **Information**
>
> You can find more detailed information about the available functions and parameters of the JavaScript report generator in the [documentation Stimulsoft Reports.JS](../../Reports_JS/index.md)and [Stimulsoft Dashboards.JS](../../Reports_JS/index.md)  products.

### Triggering JavaScript events on the Node.js server-side

When using the Node.js platform for working with reports, there is no possibility to call a JavaScript function by name, as no HTML template is used. In this case, to trigger a JavaScript event, you need to add the function itself as a string or lines of code to the handler. The event arguments will be stored in a predefined variable args, which can be used in the event code. Here’s an example of clearing the data dictionary in the template before building the report:


**index.php**

```php

<?php
    use Stimulsoft\Report\Enums\StiEngineType; 
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->engine = StiEngineType::ServerNodeJS;
    $report->onBeforeRender = 'args.report.dictionary.clear();'; 
    $report->loadFile('reports/SimpleList.mrt', true);
    $report->render();
?>
```


> **Information**
>
> The same method for JavaScript events can be used when displaying the viewer or designer without an HTML template, where it isn’t possible to predefine the necessary JavaScript function.

### Triggering PHP events on the server-side

To trigger a PHP event, you need to add the function name as a variable or the function itself to the handler. All necessary data will be passed in the event arguments. A list of available properties passed in the event arguments can be found in the [Report Engine Events](Events.md) section. Here's an example of adjusting the password in the connection string before making a data request:


**index.php**

```php

<?php
    use Stimulsoft\Events\StiDataEventArgs;
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onBeginProcessData = function (StiDataEventArgs $args) {
        args->connectionString = str_replace('Pwd=;', 'Pwd=******;', args->connectionString); 
    };
    
    $report->loadFile('reports/SimpleList.mrt', true);
    $report->render();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Rendering%20a%20Report%20from%20Code%20on%20the%20Server-Side.php).


In this example, you can retrieve and modify all the database connection parameters from the event arguments.


In a PHP server-side event, there is an option to return a textual message about the successful completion or an error in event processing, which will be displayed in the viewer or designer after the event finishes. To display an error window, you need to return the result of the function `StiResult::getError('Error message')`. To display an informational message window, you can return the result of the function `StiResult::getSuccess('Info message')` or simply the string `'Info message'`.


**index.php**

```php

<?php
    $report->onBeginProcessData = function (StiDataEventArgs $args) {
...
        return StiResult::getError('Error message');
        // return StiResult::getSuccess('Info message');
        // return 'Info message';
    };
?>
```


> **Information**
>
> If an error occurs in the event handler itself, such as a database connection error, file processing error, etc., an internal message will be displayed regardless of whether a message is defined within the event component.


> **Information**
>
> The dialog window with the message will only be shown when using the `StiViewer` or `StiDesigner` components. The report generator itself doesn’t have visual forms, so the event processing message will be displayed in the browser console.

### Triggering multiple identical events

It's possible to add an unlimited number of functions to the event handler. They will all be grouped by event type and called sequentially in the order they were added. Instead of assigning the function name, you need to use the special `append()` method, passing the function name or the function itself as a parameter.


Here’s an example of modifying an SQL query on the client-side using JavaScript and modifying the connection string on the PHP server-side:


**index.php**

```php

<?php
    use Stimulsoft\Events\StiDataEventArgs;
    use Stimulsoft\Report\StiReport;
    
    function beginProcessData(StiDataEventArgs $args) {
        $args->connectionString = str_replace('Pwd=;', 'Pwd=******;', $args->connectionString);
    };
    
    $report = new StiReport();
    $report->onBeginProcessData->append('beginProcessData'); 
    $report->onBeginProcessData->append(beginProcessData);
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
?>

...

<script>
    function beginProcessData(args) {
        args.queryString = args.queryString.replace("TableName", "Products");
    }
</script>
```

> **Information**
>
> Some events can only be triggered on the client-side using JavaScript and don’t have the option to trigger on the PHP server-side, or, they can only be triggered on the PHP server-side. When adding a function of an unsupported type to such an event, no error will occur; the added function simply will not be executed. All supported options are listed in the [Report Engine Events](Events.md) section.

### Encrypting data transferred to the PHP server

To prevent data theft by malicious actors, we recommend using the HTTPS protocol, which is sufficient in most cases. In addition to this, by default, all transmitted data is passed through a special encoding algorithm and sent to the server in encrypted form. This helps protect sensitive data, such as the login and password in the connection string, from curious users working with your application.


However, if encryption isn’t necessary, or if you need to display the original request data for debugging purposes, it is possible to disable encryption. To do this, set the `$encryptData` property to `false` in the event handler, after which all data will be transmitted in JSON format.


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->handler->encryptData = false;
    $report->process();
?>
```

### Passing GET parameter values to the PHP event handler

There’s a feature that allows the automatic transfer of all GET request parameter values to the event handler, where their values can be accessed in all events. To enable this feature, simply set the `passQueryParameters` property to `true`. After this, all GET request parameters will be passed with each request to the event handler.


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->handler->passQueryParameters = true;
    $report->process();
?>
```
