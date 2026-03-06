# Usage

To use the product, simply download the ZIP archive from the  [Downloads](https://www.stimulsoft.com/en/downloads/embedded) page of our website, extract it, and copy the contents of the /PHP folder to your web server. This folder represents a web project that includes all the necessary files and resources for the product to work, as well as examples for working with the viewer and designer.


To integrate the product into an existing project, simply copy the `/vendor` folder from the **/PHP** directory into the root directory of your project, or use the  [Composer](https://getcomposer.org/) dependency manager by running the following console command:


| **console** |
| --- |
| composer require stimulsoft/reports-php |

To work with dashboards, the following package needs to be included:


| **console** |
| --- |
| composer require stimulsoft/dashboards-php |

When using the product, in most cases, PHP code alone is sufficient to enable the primary features. For more advanced configuration and to utilize all the capabilities of the product, **JavaScript** code is required.


To use the components in a web project, you only need to connect the automatic script loader at the beginning of your PHP file. After that, you can utilize all the available PHP classes and functions to work with reports and dashboards.


**designer.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
...
?>
```

To use the designer in a web project, the `StiDesigner` class is provided. Using this class, you can create a designer object, set the necessary configurations, assign a report for editing, handle requests, and manage designer events.


Example of editing a report in the designer on an HTML page:


**designer.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Designer\StiDesigner;
    
    $designer = new StiDesigner();
    $designer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $designer->report = $report;
?>

<html>
<head>
    <?php
        $designer->javascript->renderHtml();
    ?>
</head>
<body>
    <?php
        $designer->renderHtml();
    ?>
</body>
</html>
```

The full example code is available on  [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Designer/Editing%20a%20Report%20Template%20in%20the%20Designer%20in%20an%20HTML%20template.php).


In this example, the following steps are performed sequentially:

- An instance of the StiDesigner object is created;
- The current request is processed;
- An instance of the StiReport object is created;
- A report template is loaded from the SimpleList.mrt file;
- The created report is assigned to the designer;
- The necessary JavaScript and HTML code for the component is rendered in the HTML file template.

The `$designer->process()` method processes the current request and, if successful, automatically returns the result to the client-side. More details on this can be found in the [Event Handler](../Engine/PHP_Handler.md) section.


The `$designer->javascript->renderHtml()` method renders the code required to connect the component's scripts. The `$designer->renderHtml()` method renders the JavaScript and HTML code for the component itself. Several usage options are available, which are described in detail in the [Using the Report Engine](../Engine/Usage.md) section.


Example of simplified designer rendering without using an HTML page template:


**designer.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Designer\StiDesigner;
    
    $designer = new StiDesigner();
    $designer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $designer->report = $report;
    $designer->printHtml();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Designer/Editing%20a%20Report%20Template%20in%20the%20Designer%20in%20an%20HTML%20template.php).
