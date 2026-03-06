# Showing Reports

To display a report in the viewer, simply create a `StiReport` object, load the report template into it, and assign the resulting object to the viewer. All other actions will be performed automatically, the viewer will build the report and display the first page:


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


The viewer can automatically build and display both report templates and documents (built reports), so a separate call to the report building method $report-&gt;render() is not required. Detailed instructions on working with different report and document formats can be found in the [Loading and Saving Reports](../Engine/Loading_and_Saving_Report.md) section.
