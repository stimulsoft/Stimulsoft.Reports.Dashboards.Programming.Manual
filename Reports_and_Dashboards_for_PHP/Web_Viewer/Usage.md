# Usage

To use the product, simply download the ZIP archive from the [Downloads](https://www.stimulsoft.com/en/downloads/embedded) page on our website, unpack it, and copy the contents of the **/PHP** folder to your web server. This folder is a web project that contains all the necessary files and resources for the product to function, as well as examples of how to work with the viewer and designer.


To install the product into an existing project, just copy the `/vendor` folder from **/PHP** to the root directory of your project, or use the [Composer](https://getcomposer.org/) dependency manager by running the following console command:


**console**

composer require stimulsoft/reports-php

To work with dashboards, you will need to install the following package:


**console**

composer require stimulsoft/dashboards-php

In most cases, using only PHP code is sufficient for the product to work, enabling all the core features. For more detailed product customization and to leverage all available features, JavaScript code should be used.


To use the components in a web project, simply include the automatic script loader at the beginning of the PHP file. After that, all available PHP classes and functions for working with reports and dashboards can be utilized.


**index.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
...
?>
```

The `StiViewer` class is designed to display the viewer in a web project. Using this class, you can create a viewer object, configure settings, assign a report for viewing, handle requests, and manage viewer events.


Example of displaying a report in the viewer on an HTML page:


**viewer.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $viewer->report = $report;
?>

<html>
<head>
    <?php
        $viewer->javascript->renderHtml();
    ?>
</head>
<body>
    <?php
        $viewer->renderHtml();
    ?>
</body>
</html>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).


In this example, the following steps are performed sequentially:

- A `StiViewer` object instance is created;
- The current request is processed;
- A `StiReport` object instance is created;
- The report template is loaded from the SimpleList.mrt file;
- The created report is assigned to the viewer;
- The necessary JavaScript and HTML code for the component is output in the HTML file template.


The `$viewer->process()` method processes the current request and, if successful, automatically returns the result to the client side. More details on this can be found in the [Event Handler](../Engine/PHP_Handler.md) section.


The `$viewer->javascript->renderHtml()` method outputs the code required to include the necessary component scripts. The `$viewer->renderHtml()` method outputs the JavaScript and HTML code of the component itself. There are several usage options, which are described in more detail in the [Using the Report Engine](../Engine/Usage.md) section.


Example of a simplified viewer display without using an HTML page template:


**viewer.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $viewer->report = $report;
    
    $viewer->printHtml();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).
