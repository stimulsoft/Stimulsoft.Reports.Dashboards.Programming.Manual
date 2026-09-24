# Printing Report

The viewer provides several options for printing a report, each with its own features, advantages, and disadvantages.


### Print to PDF

Printing will be done by exporting the report to PDF format. The advantages include higher accuracy in the positioning and printing of report elements compared to other printing options. One disadvantage is the requirement of a browser plugin for viewing PDF files (modern browsers have a built-in PDF viewer and print functionality).


### Print with preview

The report will be printed in a separate browser pop-up window in HTML format. The report can be previewed before printing or copied to another location as text or HTML code. Advantages include cross-browser compatibility and no need for installing special plugins. The downside is relatively lower accuracy in element positioning due to the limitations of HTML formatting.


### Print without preview

The report will be sent directly to the printer without preview. After selecting this option, the system print dialog will appear. Since printing is done in HTML format in this mode, the print quality is similar to that of printing with preview.


> **Information**
>
> Printing is handled using the browser’s built-in methods, so the print dialog may look different depending on the operating system and browser. Also, browsers do not allow JavaScript to control print settings, so the required adjustments must be made in the print dialog itself.

### Report print settings

When selecting the print option from the viewer’s toolbar, a menu with print options appears. The component allows for enforcing a specific print mode by setting the `printDestination` property to one of the values from the `StiPrintDestination` enumeration:


| **Name** | **Description** |
| --- | --- |
| `StiPrintDestination::Default` | The menu will show all available print options (this is the default property value). |
| `StiPrintDestination::Pdf` | The report will be printed in PDF format. |
| `StiPrintDestination::Direct` | The report will be printed directly in HTML format using the system print dialog. |
| `StiPrintDestination::WithPreview` | The report will be displayed in a pop-up window for preview and then printed in HTML format. |

For example, if you want to set the print mode to PDF only:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Viewer\Enums\StiPrintDestination;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->printDestination = StiPrintDestination::Pdf;
?>
```

The viewer also allows disabling the print option entirely if it's not needed. To do this, set the `showPrintButton` property to `false`:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->showPrintButton = false;
?>
```

### Report print event

If you need to perform any actions before printing a report, use the `onPrintReport` event. The event arguments contain the report print type, the export settings for printing, the page range, and the report itself. You can change the export settings, the page range, and report property values.


Example of actions performed on the JavaScript client-side before printing a report:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->onPrintReport = 'printReport';
    $viewer->process();
?>

<script>
    function printReport(args) {
        if (args.printAction == 'PrintPdf'){
            args.pageRange.rangeType = Stimulsoft.Report.StiRangeType.CurrentPage;
            args.pageRange.currentPage = 1;
        }
    }
</script>
```

Example of actions performed on the PHP server-side before printing a report:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Events\StiPrintEventArgs;
    use Stimulsoft\Report\Enums\StiRangeType;
    use Stimulsoft\Viewer\Enums\StiPrintAction;
    
    $viewer = new StiViewer();
    $viewer->onPrintReport = function (StiPrintEventArgs $args) {
        if ($args->printAction == StiPrintAction::PrintPdf){
            $args->pageRange->rangeType = StiRangeType::CurrentPage;
            $args->pageRange->currentPage = 1;
        }
    };
    $viewer->process();
?>
```

For example, when printing to PDF, you can set the image resolution and quality. By default, the `Auto` mode is used - images are printed at their original resolution.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Events\StiPrintEventArgs;
    use Stimulsoft\Viewer\Enums\StiPrintAction;
    use Stimulsoft\Export\Enums\StiImageResolutionMode;
    
    $viewer = new StiViewer();
    $viewer->onPrintReport = function (StiPrintEventArgs $args) {
        if ($args->printAction == StiPrintAction::PrintPdf) {
            $args->exportSettings->imageResolutionMode = StiImageResolutionMode::Exactly;
            $args->exportSettings->imageResolution = 300;
            $args->exportSettings->imageQuality = 1;
        }
    };
    $viewer->process();
?>
```


**viewer.php**

```php

<script>
    function printReport(args) {
        if (args.printAction == 'PrintPdf') {
            args.exportSettings.imageResolutionMode = Stimulsoft.Report.Export.StiImageResolutionMode.Exactly;
            args.exportSettings.imageResolution = 300;
            args.exportSettings.imageQuality = 1;
        }
    }
</script>
```

Detailed descriptions of the available argument values can be found in the [Viewer Events](Events.md) section.

### Printing a report from code

There’s also the option to print a report directly from code without using the viewer’s functions. Detailed instructions for this functionality can be found in the [Printing a Report from Code](../Engine/Printing_from_Code.md) section.
