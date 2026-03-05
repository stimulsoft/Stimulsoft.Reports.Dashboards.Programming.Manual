# Loading and Saving Reports

> **Information**
>
> Stimulsoft MRT and MDC files are a description of reports with XML or JSON markup. You can use MRT and MDC files, created in other Stimulsoft designers.

### Loading a report

A report can be stored as a report template (MRT file) or as a built report (MDC document) intended for further viewing or exporting. To load a report using PHP code, you can use one of the methods listed below on the StiReport object. Each method accepts either the report file name or the report itself as a string:


| **Name** | **Description** |
| --- | --- |
| `loadFile($filePath, $load = false)` | Loads a report template from an MRT file on the client-side, the path to which is specified in the function arguments. If the parameter $load is set to true, the report file will be loaded on the server side and passed to the client as a packed Base64 string. |
| `load($data, $fileName = 'Report')` | Loads a report template from an XML or JSON string and passes it to the client as a packed Base64 string. The $fileName parameter sets the file name that will be used for subsequent saving and exporting of the report. |
| `loadPacked($data, $fileName = 'Report')` | Loads and passes a report template to the client in the form of a packed Base64 string, specified in the $data parameter. The $fileName parameter sets the file name that will be used for subsequent saving and exporting of the report. |
| `loadDocumentFile($filePath, $load = false)` | Loads a built report from an MDC file on the client-side, the path to which is specified in the function parameters. If the $load parameter is set to true, the document file will be loaded on the server-side and passed to the client as a packed Base64 string. |
| `loadDocument($data, $fileName = 'Report')` | Loads a built report from an XML or JSON string and passes it to the client as a packed Base64 string. The $fileName parameter sets the file name that will be used for subsequent saving and exporting of the report. |
| `loadPackedDocument($data, $fileName = 'Report')` | Loads and passes a built report to the client in the form of a packed Base64 string, specified in the $data parameter. The $fileName parameter sets the file name that will be used for subsequent saving and exporting of the report. Loads and passes a built report to the client in the form of a packed Base64 string, specified in the $data parameter. The $fileName parameter sets the file name that will be used for subsequent saving and exporting of the report. |

Example of loading a report from a file on the server-side from a private directory and passing it to the client as a packed string for subsequent building:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt', true);
    $report->render();
?>
```

### Saving a report

In the report generation mode on the client-side JavaScript, the report generator on the PHP server-side doesn’t have access to the report object. In this case, to save a report template or document, you need to use events and JavaScript functions. More detailed information on this can be found in the "Report Engine Events" section.


An example of saving a built report as a string for future use:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->onAfterRender = 'afterRender';
    $report->loadFile('reports/SimpleList.mrt', true);
    $report->render();
?>

...

<script>
    function afterRender(args) {
        let reportJson = args.report.saveDocumentToJsonString();
...
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report%20on%20the%20Server-Side/Rendering%20a%20Report%20from%20Code%20on%20the%20Server-Side.php).


In the report-building mode on the server-side, one of the methods listed below is used to save a report:


| **Name** | **Description** |
| --- | --- |
| `saveDocument($filePath = null))` | Saves the built report as an MDC file at the path specified in the function arguments. If the `$filePath` parameter isn’t specified, the method will return the report as a JSON string instead of saving the file. |
| `savePackedDocument($filePath = null)` | Saves the built report as a packed MDZ file at the path specified in the function arguments. If the `$filePath` parameter isn’t specified, the method will return the report as a packed `Base64` string instead of saving the file. |

An example of saving a built report as a file on the server-side:


**index.php**

```php

<?php
    use Stimulsoft\Report\Enums\StiEngineType;
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->engine = StiEngineType::ServerNodeJS; 
    $report->loadFile('reports/SimpleList.mrt', true);
    $report->render();
    $report->saveDocument('reports/SimpleList.mdc');
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report%20on%20the%20Server-Side/Rendering%20a%20Report%20from%20Code%20on%20the%20Server-Side.php).


> **Information**
>
> The [Stimulsoft Reports.PHP](https://www.stimulsoft.com/en/products/reports-php) report generator and the [Stimulsoft Dashboards.PHP](https://www.stimulsoft.com/en/products/dashboards-php) analytic panels are based on the JavaScript platform and support saving MRT and MDC files only in JSON format. XML format files are only supported in load mode, and will be automatically converted to JSON format upon saving.
>
>
> Since analytic panels always require data, they can’t be saved as MDC documents. [Stimulsoft Dashboards.PHP](https://www.stimulsoft.com/en/products/dashboards-php) supports saving panels only as templates using JavaScript events and functions.
>
>
> When saving a document from the viewer menu, the file is also saved in JSON format, and has the extension MDC for a standard document, MDZ for a packed document, and MDX for an encrypted document.
