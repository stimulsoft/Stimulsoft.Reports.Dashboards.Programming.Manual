# Export Report from Code

The report generator allows exporting reports or dashboards to various formats. The table below lists all the available export formats for reports and dashboards:


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


**Data format
        
        
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

To export a report, you need to use the `exportDocument()` method of the report object.


**index.php**

```php

<?php
    use Stimulsoft\Export\Enums\StiExportFormat;
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
    $report->exportDocument(StiExportFormat::Pdf);
    $report->printHtml();
?>
```

Full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Exporting%20a%20Report%20from%20Code.php).


> **Information**
>
> Exporting a report doesn’t automatically trigger the report generation, so for a loaded report template, you must first call the `render()` method to build the report. For completed documents (already built reports), this method isn’t required.

As arguments for the `exportDocument()` method, you must specify the desired export format from the `StiExportFormat` enumeration, and optionally, the export settings. The available formats are listed in the table below:


| **Name** | **Description** |
| --- | --- |
| StiExportFormat::Document | Saving the document (built report). |
| StiExportFormat::Pdf | Saving the document (built report). |
| StiExportFormat::Xps | Saving in XPS (XML Paper Specification) format. |
| StiExportFormat::PowerPoint | Saving in Microsoft PowerPoint format. |
| StiExportFormat::Html | Saving in HTML format. |
| StiExportFormat::Html5 | Saving in HTML5 format using SVG markup elements. |
| StiExportFormat::Text | Saving in text format. |
| StiExportFormat::Word | Saving in Microsoft Word format. |
| StiExportFormat::Excel | Saving in Microsoft Excel format. |
| StiExportFormat::Odt | Saving in OpenDocument Writer format. |
| StiExportFormat::Ods | Saving in OpenDocument Calc format. |
| `StiExportFormat::Rtf` | Saving in RTF (Rich Text Format) format. |
| StiExportFormat::Csv | Saving in CSV (Comma Separated Values) data format. |
| `StiExportFormat::Json` | Saving in JSON (JavaScript Object Notation) data format. |
| `StiExportFormat::Xml` | Saving in XML (Extensible Markup Language) data format. |
| `StiExportFormat::Dbf` | Saving in DBF (dBase/FoxPro) data format. |
| `StiExportFormat::Dif` | Saving in DIF data format. |
| `StiExportFormat::Sylk` | Saving in SYLK (Symbolic Link) data format. |
| `StiExportFormat::ImagePng` | Saving in PNG (Portable Network Graphics) image format. |
| `StiExportFormat::ImageJpeg` | Saving in JPEG (Joint Photographic Experts Group) image format. |
| `StiExportFormat::ImageGif` | Saving in GIF (Graphics Interchange) image format. |
| `StiExportFormat::ImageTiff` | Saving in TIFF (Tagged Image File Format) image format. |
| StiExportFormat::ImageSvg | Saving in SVG (Scalable Vector Graphics) image format. |
| `StiExportFormat::ImageSvgz` | Saving in SVGZ (Compressed SVG) image format. |
| `StiExportFormat::ImagePcx` | Saving in PCX (Picture Exchange) image format. |
| `StiExportFormat::ImageBmp` | Saving in BMP (Windows Bitmap) image format. |

After exporting the report, the resulting data stream will be sent to the browser for download as a file. The file name and MIME type will be determined automatically. There’s also an option to display the exported report directly in the browser window (only for PDF, HTML, and images) by setting the `openAfterExport` argument to `true`.

**index.php**

```php

<?php
    $report->exportDocument(StiExportFormat::Pdf, null, true);
?>
```

### Exporting a report on the server-side

To switch the report generator to server-side mode, set the report’s engine property to `StiEngineType::ServerNodeJS`. All other events and methods for working with the report remain the same as when exporting on the client-side. When exporting on the server-side, the `exportDocument()` method will return a byte stream of the exported report.


Example of exporting a report to text format on the server-side:

**index.php**

```php

<?php
    use Stimulsoft\Export\Enums\StiExportFormat;
    use Stimulsoft\Report\Enums\StiEngineType;
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->engine = StiEngineType::ServerNodeJS;
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
    $result = $report->exportDocument(StiExportFormat::Text);
?>
```

Full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Exporting%20a%20Report%20from%20Code.php).


It’s possible to automatically save the exported report as a file on the server. To do this, specify the save path in the `filePath` argument of the export method. In this case, the `exportDocument()` method will return a boolean result indicating whether the export and file save were successful.


Example of exporting a report to Adobe PDF format on the server-side and saving the result to a specified directory:


**index.php**

```php

<?php
    use Stimulsoft\Export\Enums\StiExportFormat;
    use Stimulsoft\Report\Enums\StiEngineType;
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->engine = StiEngineType::ServerNodeJS;
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
    $exportedFilePath = 'reports/SimpleList.pdf';
    $result = $report->exportDocument(StiExportFormat::Pdf, null, false, $exportedFilePath);
?>
```

### Export report settings

When exporting a report from code, you can set the necessary export settings. Each export format has its own settings class, as listed in the table below:


| **Report Export Format** | **Settings class** |
| --- | --- |
| `StiExportFormat::Document` | No settings are provided. |
| `StiExportFormat::Pdf` | `StiPdfExportSettings()` |
| `StiExportFormat::Xps` | `StiXpsExportSettings()` |
| `StiExportFormat::PowerPoint` | `StiPowerPointExportSettings()` |
| `StiExportFormat::Html` `StiExportFormat::Html5` | `StiHtmlExportSettings()` |
| `StiExportFormat::Text` | `StiTxtExportSettings()` |
| `StiExportFormat::Word` | `StiWordExportSettings()` |
| `StiExportFormat::Excel` | `StiExcelExportSettings()` |
| `StiExportFormat::Odt` | `StiOdtExportSettings()` |
| `StiExportFormat::Ods` | `StiOdsExportSettings()` |
| `StiExportFormat::Rtf` | `StiRtfExportSettings()` |
| `StiExportFormat::Csv` `StiExportFormat::Json` `StiExportFormat::Xml` `StiExportFormat::Dbf` `StiExportFormat::Dif` `StiExportFormat::Sylk` | `StiDataExportSettings()` |
| `StiExportFormat::ImagePng` `StiExportFormat::ImageJpeg` `StiExportFormat::ImageGif` `StiExportFormat::ImageTiff` `StiExportFormat::ImageSvg` `StiExportFormat::ImageSvgz` `StiExportFormat::ImagePcx` `StiExportFormat::ImageBmp` | `StiImageExportSettings()` |


| **Dashboard Export Format** | **Settings class** |
| --- | --- |
| `StiExportFormat::Pdf` | `StiPdfDashboardExportSettings()` |
| `StiExportFormat::Html` | `StiHtmlDashboardExportSettings()` |
| `StiExportFormat::Excel` | `StiExcelDashboardExportSettings()` |
| `StiExportFormat::Csv` | `StiDataDashboardExportSettings()` |
| `StiExportFormat::ImageSvg` | `StiImageDashboardExportSettings()` |


To apply the export settings, simply pass the prepared settings object as a parameter to the report’s export method. All other actions will be handled automatically.


Example of exporting a report to Adobe PDF format on the server-side, specifying company details in the settings and disabling embedded fonts:


**index.php**

```php

<?php
    use Stimulsoft\Export\Enums\StiExportFormat;
    use Stimulsoft\Export\StiPdfExportSettings;
    use Stimulsoft\Report\Enums\StiEngineType;
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->engine = StiEngineType::ServerNodeJS;
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
    
    $settings = new StiPdfExportSettings();
    $settings->creatorString = 'My Company Name';
    $settings->keywordsString = 'SimpleList PHP Report Export';
    $settings->embeddedFonts = false;
    
    $result = $report->exportDocument(StiExportFormat::Pdf, $settings);
?>
```

Full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Exporting%20a%20Report%20from%20Code.php).


> **Information**
>
> The class of the export settings object must match the export format. Otherwise, the format returned by the `getExportFormat()` method of the export settings object will take precedence.
