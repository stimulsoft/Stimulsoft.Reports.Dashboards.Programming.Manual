# Report Export

The viewer allows exporting the displayed report or dashboard into various formats. No additional viewer settings are required for export functionality. The table below lists all available export formats for reports and dashboards:


| **Name** | **Reports** | **Dashboards** |
| --- | --- | --- |
| Document (Snapshot) | + | + |
| Adobe PDF | + | + |
| Microsoft XPS | + | - |
| Microsoft PowerPoint (.pptx) | + | - |
| HTML | + | + |
| HTML5 | + | - |
| Text | + | - |
| Microsoft Word (.docx) | + | - |
| Microsoft Excel (.xlsx) | + | + |
| OpenDocument Writer (.odt) | + | - |
| OpenDocument Calc (.ods) | + | - |
| Comma Separated Value (.csv) | + | + |
| Scalable Vector Graphics (.svg) | + | + |

### Begin export event

If you need to perform any actions before exporting a report, the `onBeginExportReport` event is provided. This event is triggered after the export settings dialog is displayed. The event arguments will include the report export type, the report itself, and all the selected export settings. Modifications to the report, its parameters, export settings, and file name are allowed.


**app.py**

```python

from stimulsoft_reports.report.enums import StiExportFormat
from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.events import StiExportEventArgs

def beginExportReport(args: StiExportEventArgs):
    if args.format == StiExportFormat.PDF:
        args.settings['imageQuality'] = 0.90
        args.settings['imageResolution'] = 200

viewer = StiViewer()
viewer.onBeginExportReport += beginExportReport
viewer.onBeginExportReport += 'beginExportReport'
```


**viewer.html**

```html

<script>
    function beginExportReport(args) {
        if (args.format == Stimulsoft.Report.StiExportFormat.Pdf) {
            args.settings.imageQuality = 0.90;
            args.settings.imageResolution = 200;
        }
    }
</script>
```

A detailed description of the available argument values can be found in the [Viewer Events](Events.md) section.

### End export event

If you need to perform any actions after exporting a report but before saving it, the `onEndExportReport` event is provided. The event arguments will include the report export type, as well as the name and byte data of the exported file. Modifications to the file name and byte data of the exported file are allowed.


**app.py**

```python

from stimulsoft_reports.report.enums import StiExportFormat
from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.events import StiExportEventArgs

def endExportReport(args: StiExportEventArgs):
    if args.format == StiExportFormat.HTML:
        htmlText = args.data

viewer = StiViewer()
viewer.onEndExportReport += endExportReport
viewer.onEndExportReport += 'endExportReport'
```


**viewer.html**

```html

<script>
    function endExportReport(args) {
        if (args.format == Stimulsoft.Report.StiExportFormat.Html) {
            htmlText = args.data
        }
    }
</script>
```

A detailed description of the available argument values can be found in the [Viewer Events](Events.md) section.

### Export settings

Sometimes it’s necessary to disable unused report export formats, leaving only the required ones. This helps streamline the interface and make the viewer easier to use. To disable unused export formats, simply set the corresponding viewer properties to `False`, for example:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.options.exports.showExportToDocument = False
viewer.options.exports.showExportToWord2007 = False
viewer.options.exports.showExportToCsv = False
```

If necessary, you can also completely hide the export dialog windows, and exporting will always be done with default settings. In this case, you can manage the settings in the export event. To disable the dialog windows, simply set the `showExportDialog` property to`False`:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.options.exports.showExportDialog = False
```

A full list of available options can be found in the [Viewer Settings](Settings.md) section.

### Exporting a report from code

It is also possible to export a report using code. This can be done with the `exportDocument()` method of the report object. A detailed description can be found in the [Exporting a Report from Code](../Engine/Export_from_Code.md) section.
