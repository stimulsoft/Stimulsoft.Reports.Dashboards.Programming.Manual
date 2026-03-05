# Creating and Editing Reports

No actions are required to launch the designer without a report. After the component loads, the designer's main menu will be displayed. If you need to start the designer with a new (empty) report, you can create a new `StiReport` object and assign it to the designer.


To edit a report in the designer, you simply need to create an `StiReport` object, load a report template into it, and assign the resulting object to the designer. All other actions will be performed automatically, and the designer will display the first page of the template.


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

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Designer/Editing%20a%20Report%20Template%20in%20the%20Designer.php).


The designer can work with standard, packed, and encrypted templates. A detailed description of working with various report formats can be found in the [Loading and Saving Reports](../Engine/Loading_and_Saving_Report.md) section.

### Report creation event

A new report can be created using the designer’s main menu. To perform any necessary actions with the new report, the `onCreateReport` event is available. This event will be triggered when a new empty report is created from the main menu or when a report is created using a wizard. The event arguments will contain the report object created in the designer. If necessary, you can modify it, connect data, or load a pre-prepared report template. After the event is completed, this report will be automatically loaded into the designer for editing.


Example of connecting data and synchronizing the data dictionary when creating a new report:


**designer.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Designer\StiDesigner;
    
    $designer = new StiDesigner();
    $designer->onCreateReport = 'createReport';
    $designer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $designer->report = $report;
?>

...

<script>
    function createReport(args) {
        let dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
        dataSet.readJsonFile("Data/Demo.json");
        
        args.report.regData(dataSet.dataSetName, "", dataSet);
        args.report.dictionary.synchronize();
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).


If needed, the process of creating a new report can be controlled on the PHP server-side. Example of modifying new report parameters on the PHP server-side:


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner;
    use Stimulsoft\Events\StiReportEventArgs;
    
    $designer = new StiDesigner();
    $designer->onCreateReport = function (StiReportEventArgs $args) {
        $args->report->ReportAlias = 'New Report Alias';
    };
    
    $designer->process();
    $designer->printHtml();
?>
```

Example of loading a pre-prepared template with pre-configured data connections:


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner;
    use Stimulsoft\Events\StiReportEventArgs;
    
    $designer = new StiDesigner();
    $designer->onCreateReport = function (StiReportEventArgs $args) {
        $reportJson = file_get_contents('reports/NewTemplateWithData.mrt');
        $args->setReportJson($reportJson);
    };
    
    $designer->process();
    $designer->printHtml();
?>
```

A detailed description of available argument values can be found in the [Designer Events](Events.md) section.
