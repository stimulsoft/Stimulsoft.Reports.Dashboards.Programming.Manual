# Usage

To use the product, simply download the ZIP archive from the [Downloads](https://www.stimulsoft.com/en/downloads/embedded) page on our website, extract it, and copy the contents of the **/PHP** folder to your web server. This folder represents a web project containing all the necessary files and resources for the product to function, as well as examples for working with the viewer and designer.


To install the product into an existing project, simply copy the `/vendor` folder from the **/PHP** directory to the root directory of your project, or use the [Composer](https://getcomposer.org/) dependency manager by running the following console command:


**console**

composer require stimulsoft/reports-php

To work with dashboards, you will need to include the following package:


**console**

composer require stimulsoft/dashboards-php

When using the product, in most cases, it is sufficient to use only PHP code, which provides the functionality for all the basic features. For more detailed configuration and to utilize all the features, JavaScript code needs to be used.


To use the components in a web project, simply include the script autoloader at the beginning of the PHP file. After that, you can use all available PHP classes and functions to work with reports and dashboards:


**index.php**

```php

<?php
    require_once 'vendor/autoload.php';
    ...
?>
```

The class `StiReport` is designed for working with the report generator. Using this class, you can load a report template or document, perform report building and exporting, handle requests, and manage report generator events. For example, to load a report from a file, build it, and display a message in the browser window:


**index.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onAfterRender = 'afterRender';
    $report->process();
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
?>

<html>
    <head>
        <?php
            $report->javascript->renderHtml();
        ?>
        <script type="text/javascript">
            function afterRender() {
                alert('Done!');
            }
        </script>
    </head>
    <body>
        <?php
            $report->renderHtml();
        ?>
    </body>
</html>
```

The complete code sample can be found on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


In this example, the following steps are performed sequentially:

- An instance of the `StiReport` object is created;
- Necessary event handlers are added;
- The current request is processed;
- The report template is loaded from the file `SimpleList.mrt`;
- The report building command is called;
- In the HTML file template, JavaScript event code is added, and the necessary JavaScript and HTML code for the component is rendered.


The `$report->process()` method processes the current request and, upon success, automatically returns the result to the client-side. This is explained in more detail in the [Event Handler](PHP_Handler.md) section.


The `$report->javascript->renderHtml()` method outputs the code for including the necessary component scripts. The `$report->renderHtml()` method outputs the JavaScript and HTML code for the component itself.


Our products, [Stimulsoft Reports.PHP](https://www.stimulsoft.com/en/products/reports-php) and [Stimulsoft Dashboards.PHP](https://www.stimulsoft.com/en/products/dashboards-php), do not have a native report generator core in PHP. Report building and exporting are performed using JavaScript on the client side or on the server side with the Node.js platform. Therefore, when using PHP code to work with the components, you need to call one of the special methods, which will add the corresponding JavaScript code to the web page for performing all necessary actions, as well as the HTML code for the visual part of the component.


| **Name** | **Description** |
| --- | --- |
| `getHtml($mode = StiHtmlMode::HtmlScripts)` | Returns the JavaScript and HTML code necessary for the component to function, including all required actions on the report. The `$mode` parameter allows you to set different options for the returned code: - `StiHtmlMode::Scripts` – only the necessary JavaScript code for insertion into the `<script></script>` block on an HTML page; - `StiHtmlMode::HtmlScripts` – the necessary JavaScript and HTML code for insertion into an HTML element on the page; - `StiHtmlMode::HtmlPage` – a fully prepared HTML page. **Note:** For component elements, such as the `$report->javascript` object, the `getHtml()` method does not accept parameters since it has only one output option. |
| `renderHtml($elementId = null)` | This method outputs the JavaScript and HTML code required for the component to function, including all necessary actions on the report. The `$elementId` parameter allows you to specify the ID of the HTML element on the page where the component will be rendered. By default, the output is rendered in the current location of the page. |
| `printHtml()` | The method can output a fully prepared HTML page with all the necessary scripts for the component to work. The current HTML page template is completely ignored. This mode is ideal for full-screen viewing or editing of the report. |

Thus, the methods described above allow you to display the component in different ways depending on the requirements. Here’s an example of simplified component rendering without using an HTML page template:


**index.php**

```php

<?php
    require_once 'vendor/autoload.php';
    
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onAfterRender = "alert('Done!');";
    $report->process();
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
    $report->printHtml();
?>
```


**Information**


When using the Node.js platform for report generation on the PHP server side, the specified methods will be called automatically within the handler, and their explicit use is not required.

### Managing URLs for Loading Report Generator JavaScript Files

By default, all product JavaScript files are loaded via URLs relative to the location of the current PHP script. In some cases, this behavior needs to be changed, and several options are provided for this. To use an absolute path for loading all product scripts, set the `useRelativeUrls` option to `false`:


**index.php**


<?php
use Stimulsoft\Report\StiReport;
$report = new StiReport();$report->javascript->useRelativeUrls = false;
?>

To adjust the relative path, the `relativePath` option is provided. You need to assign a string value that will be used when forming the URL for loading the scripts. In this case, the `useRelativeUrls` option must be enabled (default value):


**index.php**


<?php
use Stimulsoft\Report\StiReport;
$report = new StiReport();$report->javascript->relativePath = '../../';
?>

By default, the scripts are loaded as static files. To enable dynamic script loading using a PHP handler, set the `useStaticUrls` option to `false`:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->javascript->useStaticUrls = false;
?>
```


> **Information**
>
> The report viewer and report designer components also have a `javascript` property, allowing you to manage script settings in the same way as described above.

Various alternatives of deployment and optimization are considered in the [Optimization of script loading chapter](Optimazing_scripts_loading.md).
