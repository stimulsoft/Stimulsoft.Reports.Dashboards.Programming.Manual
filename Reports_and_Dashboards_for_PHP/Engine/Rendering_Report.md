# Rendering a Report

To build a loaded report, you should call the `render()` function on the report object. For example, you want to build a report before exporting it.


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Export\Enums\StiExportFormat;

    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
    $report->exportDocument(StiExportFormat::Pdf);
    $report->printHtml();
?>
```

The full example code is available on[GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


To perform any actions with the report before building it using JavaScript, you can simply define the name of a JavaScript function for the `onBeforeRender` event. The event's arguments will include the action type and the report itself. Example of registering JSON data before report generation:


**index.php**

```php


<?php
    use Stimulsoft\Report\StiReport;

    $report = new StiReport();
    $report->onBeforeRender = 'beforeRender'; 
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
?>

...

<script>
    function beforeRender(args) {
        let dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
        dataSet.readJsonFile("Demo.json");

        let report = args.report;
        report.regData(dataSet.dataSetName, "", dataSet);
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


To perform any actions after building the report using JavaScript, you can define the name of a JavaScript function for the `onAfterRender` event. The event's arguments will include the action type and the report itself. Example of displaying a message after report generation:


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
        alert("The report rendering is completed.");
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).
