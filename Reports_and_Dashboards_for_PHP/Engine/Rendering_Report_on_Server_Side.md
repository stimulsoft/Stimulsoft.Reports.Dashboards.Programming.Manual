# Rendering a Report on Server Side

To build a report on the server-side, the universal Node.js platform is used. This platform executes the necessary block of JavaScript code and returns the prepared result.


**Deploying the Node.js Platform**

Before using the report generator on the server-side, you need to install the Node.js platform and configure it. This can be done separately by following the Node.js installation instructions for a specific operating system from the [official platform website](https://nodejs.org/en), or automatically using a special deployment function.
If the platform is already installed, it is enough to specify the path to the directory containing the executable files of the platform. If necessary, you can also specify the path to the working directory, where the required Node.js packages will be installed in the node_modules subdirectory:


**index.php**

```php

<?php
    use Stimulsoft\StiNodeJs;

    $nodejs = new StiNodeJs();
    
    //$nodejs->binDirectory = "C:\\Program Files\\nodejs";
    //$nodejs->binDirectory = "/usr/bin/nodejs";
    //$nodejs->workingDirectory = "";
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


If the platform and packages aren’t installed, special methods can be used to install them. These methods need to be called only once: the first method installs the Node.js platform itself, and the second method installs or updates all necessary packages to the latest version:


**index.php**

```php

<?php
    use Stimulsoft\StiNodeJs;

    $nodejs = new StiNodeJs();

    $result = $nodejs->installNodeJS();
    if ($result)
        $result = $nodejs->updatePackages();
    
    $message = $result ? 'The installation was successful.' : $nodejs->error;
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


The platform and packages will be installed in the specified working directory.

### Building a report

To switch the report generator to server-side operation, you need to set the report's engine property to `StiEngineType::ServerNodeJS`. The rest of the events and methods for working with the report are exactly the same as when building a report on the client-side.
After calling the `render()` method on the report object, the built report can be saved using the `saveDocument()` or `savePackedDocument()` methods, as described in the [Loading and Saving a Report](Loading_and_Saving_Report.md) section. Additionally, after building the report, it can be exported to one of many formats using the `exportDocument()` method, as described in the [Exporting a Report from Code](Export_from_Code.md) section.
Example of loading and building a report template, and subsequently saving the built report to a file on the server-side:


**index.php**

```php

<?php
    use Stimulsoft\Report\Enums\StiEngineType;
    use Stimulsoft\Report\StiReport;$report = new StiReport();$report->engine = StiEngineType::ServerNodeJS; $report->loadFile('reports/SimpleList.mrt', true);$report->render();$report->saveDocument('reports/SimpleList.mdc');
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


Any errors that occur when working with Node.js packages, as well as when building and exporting a report on the server-side, can be read in the `report->nodejs->error` and `report->nodejs->errorStack` properties. These properties will contain the last error in the queue:


**index.php**

```php

<?php
    use Stimulsoft\Report\Enums\StiEngineType;
    use Stimulsoft\Report\StiReport;$report = new StiReport();$report->engine = StiEngineType::ServerNodeJS; $report->loadFile('reports/SimpleList.mrt', true);$report->render();
    if (!$report) {
        // The main text of the error as a string.
        $error = $report->nodejs->error;
        // The full error text as an array of strings.
        $errorStack = $report->nodejs->errorStack;
    }
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).
