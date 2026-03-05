# Optimization of Scripts Loading

Due to the extensive functionality of the product, the scripts have a relatively large size. During the initial load of a web application, or if browser caching is disabled, loading may take some time, especially with slow internet connections. We offer two solutions to this problem: using packed scripts or utilizing partial functionality and loading only the required components. It is possible to combine these options.

### Packed scripts

Packed scripts have the same structure as regular scripts but end with `*.pack.js` in the file name. These scripts contain a block of packed data in the form of a JavaScript variable and a compact unpacker. When all scripts are loaded, the unpacker automatically unpacks all the loaded data and executes the prepared script. Unpacking takes some time, but under certain circumstances—such as with a slow internet connection—this time is significantly shorter than the time it would take to load regular scripts.


To use packed scripts you should set the `$js->packed` to `true`. For example:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->javascript->usePacked = true;
?>
```

### Partial loading of scripts

The `stimulsoft.reports.js` script contains all the functionality for report building and exporting. If you only need specific features for generating reports, partial script loading is available, allowing you to load only the necessary parts of the generator that contain specific features. For example, if your reports do not use maps, you can skip loading that functionality, which will speed up the loading of your web project and reduce browser memory consumption.


> **Information**
>
> This option is only available for the report generator core. The viewer and designer cannot be split into parts; their scripts will always be loaded as a single block.

To use partial script loading, simply configure the appropriate options in the `javascript` property of the report object.


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->javascript->reportsChart = true;
    $report->javascript->reportsExport = true;
    $report->javascript->reportsImportXlsx = true;
    $report->javascript->reportsMaps = false;
    $report->javascript->blocklyEditor = false;
?>
```

Each PHP option of the StiJavaScript object controls the loading of a script containing specific functionality. The table contains the whole set of scripts, which you can load separately.


| **Name** | **Description** |
| --- | --- |
| `javascript->reportsExport` | Contains algorithms for exporting generated reports into various formats such as PDF, HTML, Excel, RichText, and others. |
| `javascript->reportsChart` | Includes components for working with all types of charts in the report. |
| `javascript->reportsMaps` | Contains components for working with regional and online maps. |
| `javascript->blocklyEditor` | Contains a visual editor based on Blockly for creating event scripts in the report. The event handler itself is built into the report engine. |
| `javascript->reportsImportXlsx` | Contains algorithms for working with Excel data sources. |


> **Information**
>
> The report viewer and report designer components also have a `javascript` property, which allows you to manage script settings in the same way as described above. This enables control over which scripts are loaded and optimizes performance by customizing the functionality required for these components.
