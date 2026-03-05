# Report Export

The viewer allows exporting displayed reports or dashboards into various formats. No additional viewer configuration is required for exporting. The table below lists all available export formats for reports and dashboards:

| **Export format** | **Reports** | **Dashboards** |
| --- | --- | --- |
| Document (Snapshot) | + | + |
| Adobe PDF | + | + |
| XPS (XML Paper Specification) | + | - |
| Microsoft PowerPoint | + | - |
| HTML | + | + |
| HTML5 | + | - |
| Text | + | - |
| Microsoft Word | + | - |
| Microsoft Excel | + | + |
| OpenDocument Writer | + | - |
| OpenDocument Calc | + | - |
| RTF (Rich Text Format) | + | - |


| **Data format** | **Reports** | **Dashboards** |
| --- | --- | --- |
| CSV (Comma Separated Value) | + | + |
| JSON (JavaScript Object Notation) | + | + |
| XML (Extensible Markup Language) | + | + |
| DBF (dBase/FoxPro) | + | + |
| DIF | + | + |
| SYLK (Symbolic Link) | + | + |


| **Image format** | **Reports** | **Dashboards** |
| --- | --- | --- |
| PNG (Portable Network Graphics) | + | + |
| JPEG (Joint Photographic Experts Group) | + | + |
| GIF (Graphics Interchange) | + | + |
| TIFF (Tagged Image File Format) | + | + |
| SVG (Scalable Vector Graphics) | + | + |
| SVGZ (Compressed SVG) | + | + |
| PCX (Picture Exchange) | + | + |
| BMP (Windows Bitmap) | + | + |

**Begin export event**

If any actions need to be performed before exporting a report, the `onBeginExportReport` event is used. This event is triggered after the export settings dialog is shown. The event arguments include the export type, export file name, the report itself, and the settings for the selected export format. You can modify the report properties, export settings, and file name.


Example of performing actions on the client JavaScript before exporting a report:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->onBeginExportReport = 'beginExportReport';
    $viewer->process();
?>

...

<script>
    function beginExportReport(args) {
        if (args.format == Stimulsoft.Report.StiExportFormat.Pdf) {
            args.settings.creatorString = 'My Company Name';
            args.settings.embeddedFonts = false;
        }
    }
</script>
```

Example of performing actions on the server PHP side before exporting a report:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Events\StiExportEventArgs;
    use Stimulsoft\Export\Enums\StiExportFormat;
    use Stimulsoft\Export\StiPdfExportSettings;
    
    $viewer = new StiViewer();
    $viewer->onBeginExportReport = function (StiReportEventArgs $args) {
        $args->fileName = "MyExportedFileName.$args->fileExtension";
        
        if ($args->format == StiExportFormat::Pdf) {
            /** @var StiPdfExportSettings $settings */
            $settings = $args->settings;
            $settings->creatorString = 'My Company Name';
            $settings->embeddedFonts = false;
        }  
    };
    $viewer->process();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).


Detailed descriptions of the available event arguments can be found in the [Viewer Events](Events.md) section. A detailed explanation of the available export settings is found in the [Exporting a Report from Code](../Engine/Export_from_Code.md) section.

**End export event**

If any actions need to be performed after a report is exported but before it’s saved, the `onEndExportReport` event is used. The event arguments include the export type, file name, and the byte data of the exported file. You can modify the file name and byte data of the exported file.


Example of performing actions on the client JavaScript side after exporting a report:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->onEndExportReport = 'endExportReport';
    $viewer->process();
?>

...

<script>
    function endExportReport(args) {
        if (args.format == Stimulsoft.Report.StiExportFormat.Html) {
            let fileName = args.fileName;
            let htmlText = args.data;
        }
    }
</script>
```

Example of performing actions on the server PHP side after exporting a report:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Events\StiExportEventArgs;
    use Stimulsoft\Export\Enums\StiExportFormat;
    
    $viewer = new StiViewer();
    $viewer->onEndExportReport = function (StiReportEventArgs $args) {
        $fileName = $args->fileName; 
        if ($args->format == StiExportFormat::Pdf) {
            $htmlText = base64_decode($args->data);
        }  
    };
    $viewer->process();
?>
```


> **Information**
>
> Byte data is sent to the server in `Base64` encoding, so it must be decoded back to its original byte stream using a standard PHP function like `base64_decode()` before saving.

Detailed descriptions of the available event arguments can be found in the [Viewer Events](../Settings.md) section.

**Export settings**

Sometimes it is necessary to disable unused report export formats and leave only the required ones. This simplifies the interface and makes the viewer easier to use. To disable unused export formats, simply set the corresponding viewer properties to `false`. For example:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->exports->showExportToDocument = false;
    $viewer->options->exports->showExportToWord = false;
    $viewer->options->exports->showExportToCsv = false;
?>
```

Additionally, you can completely disable the export dialog windows, and exporting will always be done with default settings. You can manage these settings in the export event. To disable the export dialogs, set the `showExportDialog` property to `false`:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->exports->showExportDialog = false;
?>
```

The full list of available options is in the [Viewer Settings](../Settings.md) section.

**Exporting a report from code**

To export a report directly from code without using the viewer, a special method `exportDocument()` is available for the report object. Detailed instructions are provided in the [Exporting a Report from Code](../Engine/Export_from_Code.md) section.
