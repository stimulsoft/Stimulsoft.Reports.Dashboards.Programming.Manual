# Preview

The designer provides a preview mode for the editable report. To do this, simply switch to the corresponding tab in the designer window. The report template will be generated and displayed in the built-in viewer.

**Preview event**

Before previewing the report, there’s an option to perform necessary actions, such as connecting data for the report. For this, there is a special `onPreviewReport` event, which will be triggered before the report is previewed. The event arguments will contain the report intended for preview.


Example of connecting data on the client-side using JavaScript for report preview:


**designer.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Designer\StiDesigner;
    
    $designer = new StiDesigner();
    $designer->onPreviewReport = 'previewReport';
    $designer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $designer->report = $report;
?>

...

<script>
    function previewReport(args) {
        let dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
        dataSet.readJsonFile("Data/Demo.json");
        
        args.report.regData(dataSet.dataSetName, "", dataSet);
    }
</script>
```

Example of modifying report properties on the PHP server-side before report preview:


**designer.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Designer\StiDesigner;
    
    $designer = new StiDesigner();
    $designer->onPreviewReport = function (StiReportEventArgs $args) {
        $args->report->ReportDescription = 'This is a report description from the PHP server-side.';
    };
    
    $designer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $designer->report = $report;
    
    $designer->printHtml();
?>
```

A detailed description of the available event arguments can be found in the [Designer Events](Events.md) section.

**Additional options**

The report preview window in the designer is a fully interactive viewer that allows printing and exporting the report and supports working with report parameters. All interactive actions, such as dynamic sorting, drill-down, and collapsing, are supported. No additional settings are required to use these features in the report designer.
