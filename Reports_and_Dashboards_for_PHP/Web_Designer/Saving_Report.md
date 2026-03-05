# Saving Reports

The designer provides two options for saving a report, which are available in the main menu and on the designer's main panel: **Save** and **Save As**. Each of these saving options has its own modes and settings.

**Saving a report on the client-side via JavaScript**

When the **Save** button is pressed, the report template file is saved using browser mechanisms, and no settings are required for this. If you need to save the report using your own methods, the `onSaveReport` event is available. The event arguments will include the report file name and the report itself. The report can be saved, for example, as a JSON string and sent to the server using your own methods.


Example of saving a report as a JSON string on the client-side via JavaScript for further use in the application:


**designer.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Designer\StiDesigner;
    
    $designer = new StiDesigner();
    $designer->onSaveReport = 'saveReport';
    $designer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $designer->report = $report;
?>

...

<script>
    function saveReport(args) {
        let fileName = args.fileName;
        let report = args.report;
        let reportJson = args.report.saveToJsonString();
        ...
    }
</script>
```

If necessary, after saving the report, you can display a dialog with an error message or text notification. For this, the special function `StiError.showError()` is available. You can decide whether to display the error message.


**designer.php**

```php

<script>
    function saveReport(args) {
        let report = args.report;
        
        // Error message
        Stimulsoft.System.StiError.showError("An error occurred while saving the report.");
        
        // Info message
        Stimulsoft.System.StiError.showError("The report was saved successfully.", true, true);
    }
</script>
```

When the **Save As** button is pressed, a dialog box will be displayed requesting the report file name. After that, the report template file will be saved using browser mechanisms. If you need to save the report using your own methods, the `onSaveAsReport` event is available. The event arguments will include the report file name and the report itself.


The functionality of this event is no different from the `onSaveReport` event, except that after the event is completed, the report template will be automatically saved on the computer using the browser. To prevent this action, simply set the `preventDefault` property to `true` in the event arguments, and the automatic saving will not be performed.


**designer.php**

```php

<script>
    function saveReport(args) {
        args.preventDefault = true;
    }
</script>
```

If necessary, you can access the original report name or the name from the save dialog as follows:


**designer.php**

```php

<script>
    function saveReport(args) {
        // Report name from the designer save dialog
        let reportName1 = args.fileName;
        
        // Original report name from properties
        let reportName2 = args.report.reportName;
    }
</script>
```

A detailed description of available argument values can be found in the [Designer Events](Events.md) section.


**Saving a report on the PHP server-side**

To save a report on the PHP server-side, you simply need to define the `onSaveReport` event. The event arguments will include the report file name and the report itself as an object. You can use standard PHP functions to save the report.


Example of saving an editable report as a file in a specified directory:


**designer.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\Designer\StiDesigner;
    use Stimulsoft\Events\StiReportEventArgs;
    
    $designer = new StiDesigner();
    $designer->onSaveReport = function (StiReportEventArgs $args) {
        $reportJson = $args->getReportJson();
        file_put_contents('reports/' . $reportFileName, $reportJson);
    };
    
    $designer->process();
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt'); 
    $designer->report = $report;
    
    $designer->printHtml();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Designer/Saving%20a%20Report%20Template%20on%20the%20Server-Side.php).


A detailed description of available argument values can be found in the [Designer Events](Events.md) section.


> **Information**
>
> Similarly, the `onSaveAsReport` event works on the PHP server-side, and all event arguments have the same names and values.
