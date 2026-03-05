# Exporting a Report From Code

The reporting tool allows you to export the generated report or dashboard to various formats. Below is a list of all available export formats for reports and dashboards:


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


**Export format
        
        
          Reports
        
        
          Dashboards

          CSV (Comma Separated Value)
        
        
          +
        
        
          +

          JSON (JavaScript Object Notation)
        
        
          +
        
        
          +

          XML (Extensible Markup Language)
        
        
          +
        
        
          +

          DBF (dBase/FoxPro)
        
        
          +
        
        
          +

          DIF
        
        
          +
        
        
          +

          SYLK (Symbolic Link)
        
        
          +
        
        
          +**


| **Export format** | **Reports** | **Dashboards** |
| --- | --- | --- |
| PNG (Portable Network Graphics) | + | + |
| JPEG (Joint Photographic Experts Group) | + | + |
| GIF (Graphics Interchange) | + | + |
| TIFF (Tagged Image File Format) | + | + |
| SVG (Scalable Vector Graphics) | + | + |
| SVGZ (Compressed SVG) | + | + |
| PCX (Picture Exchange) | + | + |
| BMP (Windows Bitmap) | + | + |

To export a report, you should utilize the special `exportDocument()` function on the report object.


**app.py**

```python

from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiExportFormat

report = StiReport()
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
report.exportDocument(StiExportFormat.PDF)
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


> **Information**
>
> Exporting a report doesn't automatically trigger its construction. Therefore, the loaded report template must first call the `render()` method, which build the report. For generated reports, calling the specified function is not necessary.

As arguments to the `exportDocument()` function, you should specify the required export format from the `StiExportFormat` enumeration. The available format options are as follows:


| **Name** | **Description** |
| --- | --- |
| `StiExportFormat.DOCUMENT` | Saves the rendered document. |
| `StiExportFormat.PDF` | Saves to Adobe PDF. |
| `StiExportFormat.XPS` | Saves to XPS (XML Paper Specification). |
| `StiExportFormat.POWERPOINT` | Saves to Microsoft PowerPoint. |
| `StiExportFormat.HTML` | Saves to HTML. |
| `StiExportFormat.HTML5` | Saves to HTML5, using SVG markup elements. |
| `StiExportFormat.TEXT` | Saves to text. |
| `StiExportFormat.WORD` | Saves to Microsoft Word. |
| `StiExportFormat.EXCEL` | Saves to Microsoft Excel. |
| `StiExportFormat.ODT` | Saves to OpenDocument Text. |
| `StiExportFormat.ODS` | Saves to OpenDocument Spreadsheet. |
| `StiExportFormat.RTF` | Saving in RichText format. |
| `StiExportFormat.CSV` | Saves to CSV (Comma-Separated Values). |
| `StiExportFormat.JSON` | Saving data in JSON format. |
| `StiExportFormat.XML` | Saving data in XML format |
| `StiExportFormat.DBF` | Saving data in DBF format. |
| `StiExportFormat.DIF` | Saving data in DIF format. |
| `StiExportFormat.SYLK` | Saving in SYLK data format. |
| `StiExportFormat.IMAGE_PNG` | Save as PNG image. |
| `StiExportFormat.IMAGE_JPEG` | Saving to JPEG format image. |
| `StiExportFormat.IMAGE_GIF` | Saving to GIF format image. |
| `StiExportFormat.IMAGE_TIFF` | Saving to TIFF format image. |
| `StiExportFormat.IMAGE_SVG` | Saves to SVG. |
| `StiExportFormat.IMAGE_SVGZ` | Saving to SVGZ format image. |
| `StiExportFormat.IMAGE_PCX` | Saving to PCX format image. |
| `StiExportFormat.IMAGE_BMP` | Saving to BMP image format. |

After exporting a report, the resulting data stream will be sent to the browser for download as a file. The file name and MIME type will be determined automatically. There is also an option to display the exported report directly in the browser window (available only for PDF, HTML, and image formats). To enable this, set the `openAfterExport` argument to `True`:


**app.py**

```python
...

report.exportDocument(StiExportFormat.PDF, openAfterExport = True)
```


**Exporting a report on the server-side**
To switch the report generator to server-side mode, set the report’s `engine` property to `StiEngineType.SERVER_NODE_JS`. The rest of the events and methods for working with the report remain the same as when exporting on the client side. When exporting on the server side, the `exportDocument()` method returns a byte stream of the exported report.


Example of exporting a report to PDF format on the server side:


**app.py**

```python

from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiEngineType, StiExportFormat 

report = StiReport()
report.engine = StiEngineType.SERVER_NODE_JS
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
bytes = report.exportDocument(StiExportFormat.PDF)
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


You can also automatically save the exported report as a file on the server. To do this, specify the save path using the `filePath` argument of the export method. In this case, the `exportDocument()` method will return a boolean indicating the success of the export and save operation.


An example of exporting a report to PDF format on the server side and saving the result to the specified directory:


**app.py**

```python
...

exportedFilePath = url_for('static', filename='reports/SimpleList.pdf')
bytes = report.exportDocument(StiExportFormat.PDF, filePath = exportedFilePath)
```

### Report export settings

When exporting a report from code, you can apply custom export settings. Each export format has its own settings class, listed in the table below:


| **Report export format** | **Settings class** |
| --- | --- |
| `StiExportFormat.DOCUMENT` | No settings are provided. |
| `StiExportFormat.PDF` | `StiPdfExportSettings()` |
| `StiExportFormat.XPS` | `StiXpsExportSettings()` |
| `StiExportFormat.POWERPOINT` | `StiPowerPointExportSettings()` |
| `StiExportFormat.HTML` `StiExportFormat.HTML5` | `StiHtmlExportSettings()` |
| `StiExportFormat.TEXT` | `StiTxtExportSettings()` |
| `StiExportFormat.WORD` | `StiWordExportSettings()` |
| `StiExportFormat.EXCEL` | `StiExcelExportSettings()` |
| `StiExportFormat.ODT` | `StiOdtExportSettings()` |
| `StiExportFormat.ODS` | `StiOdsExportSettings()` |
| `StiExportFormat.RTF` | `StiRtfExportSettings()` |
| `StiExportFormat.CSV` `StiExportFormat.JSON` `StiExportFormat.XML` `StiExportFormat.DBF` `StiExportFormat.DIF` `StiExportFormat.SYLK` | `StiDataExportSettings()` |
| `StiExportFormat.IMAGE_PNG` `StiExportFormat.IMAGE_JPEG` `StiExportFormat.IMAGE_GIF` `StiExportFormat.IMAGE_TIFF` `StiExportFormat.IMAGE_SVG` `StiExportFormat.IMAGE_SVGZ` `StiExportFormat.IMAGE_PCX` `StiExportFormat.IMAGE_BMP` | `StiImageExportSettings()` |


| **Dashboard export format** | **Settings class** |
| --- | --- |
| StiExportFormat.PDF | StiPdfDashboardExportSettings() |
| StiExportFormat.HTML | StiHtmlDashboardExportSettings() |
| StiExportFormat.EXCEL | StiExcelDashboardExportSettings() |
| StiExportFormat.CSV | StiDataDashboardExportSettings() |
| StiExportFormat.IMAGE_SVG | StiImageDashboardExportSettings() |


To apply export settings, pass the configured settings object as a parameter to the report's export method. All other actions will be performed automatically.


An example of exporting a report to PDF format on the server side, the settings specify company information and allow editing:


**app.py**

```python

from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiEngineType, StiExportFormat
from stimulsoft_reports.export import StiPdfExportSettings
from stimulsoft_reports.export.enums import StiPdfAllowEditable

report = StiReport()
report.engine = StiEngineType.SERVER_NODE_JS
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()

settings = StiPdfExportSettings()
settings.creatorString = 'Stimulsoft'
settings.allowEditable = StiPdfAllowEditable.YES

bytes = report.exportDocument(StiExportFormat.PDF, settings)
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


> **Information**
>
> The export settings object class must match the export format. Otherwise, the format returned by the `getExportFormat()` method of the export settings object will take precedence.
