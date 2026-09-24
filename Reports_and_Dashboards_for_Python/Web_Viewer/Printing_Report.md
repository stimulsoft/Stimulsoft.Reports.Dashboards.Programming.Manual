# Printing a Report

The viewer provides several options for printing a report, each with its own features, advantages, and disadvantages.


### Print to PDF

Printing is done by exporting the report to PDF format. The advantages include higher accuracy in the placement and printing of report elements compared to other printing options. A disadvantage is the requirement of a PDF viewer plugin installed in the browser (modern browsers typically have built-in tools for viewing and printing PDF files).


### Print with preview

The report is printed in a separate browser popup window in HTML format. The report can be previewed before sending it to the printer or copied as text or HTML code. Advantages include cross-browser compatibility for printing and no need for special plugins. The disadvantage is the relatively low accuracy in the placement of report elements due to the specifics of HTML formatting. The report is printed in a separate browser popup window in HTML format. The report can be previewed before sending it to the printer or copied as text or HTML code. Advantages include cross-browser compatibility for printing and no need for special plugins. The disadvantage is the relatively low accuracy in the placement of report elements due to the specifics of HTML formatting.


### Print without preview

The report is printed directly to the printer without a preview. After selecting this menu option, the system print dialog is displayed. Since the report is printed in HTML format in this mode, the print quality is similar to that of printing with a preview.


> **Information**
>
> Report printing is carried out using the built-in methods of the browser in use, so the appearance of the print dialog window may vary across different operating systems and browsers. Additionally, the browser doesn’t allow control over print settings through JavaScript code, so the necessary settings must be configured directly in the print dialog window.

### Report print settings

When selecting report printing from the viewer's toolbar, a menu with print options is displayed. The component can forcibly set the required print mode. To do this, simply set the `printDestination` property to one of the values listed below from the `StiPrintDestination` enumeration:


| **Name** | **Description** |
| --- | --- |
| `StiPrintDestination.DEFAULT` | When printing is selected, a menu with available print options will be displayed (this is the default property value). |
| `StiPrintDestination.PDF` | Print to PDF format. |
| `StiPrintDestination.DIRECT` | Print to HTML format directly to the printer, displaying the system print dialog. |
| `StiPrintDestination.WITH_PREVIEW` | Print to HTML format with a preview in a popup window. Print to HTML format with a preview in a popup window. |

For example, to set the print mode to PDF format only:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.viewer.enums import StiPrintDestination

viewer = StiViewer()
viewer.options.toolbar.printDestination = StiPrintDestination.PDF
```

The viewer provides the option to completely disable report printing if it isn’t needed. To do this, set the `showPrintButton` property to `False`.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.options.toolbar.showPrintButton = False
```

### Report print event

If you need to perform any actions before printing a report, use the `onPrintReport` event. The event arguments contain the report print type, the export settings for printing, the page range, and the report itself. You can change the export settings, the page range, and report property values.


For example, when printing to PDF, you can set the image resolution and quality. By default, the `Auto` mode is used - images are printed at their original resolution.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.viewer.enums import StiPrintAction
from stimulsoft_reports.events import StiPrintEventArgs
from stimulsoft_reports.export.enums import StiImageResolutionMode

def printReport(args: StiPrintEventArgs):
    if args.printAction == StiPrintAction.PRINT_PDF:
        args.exportSettings.imageResolutionMode = StiImageResolutionMode.EXACTLY
        args.exportSettings.imageResolution = 300
        args.exportSettings.imageQuality = 1

viewer = StiViewer()
viewer.onPrintReport += printReport
```


**viewer.html**

```html

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

A detailed description of the available argument values can be found in the [Viewer Events](Events.md) section.

### Printing a report from code

It is possible to print a report directly from code without using the viewer functions. A detailed description of this functionality can be found in the report generator section Printing a [Report from Code](../Engine/Printing_from_Code.md).
