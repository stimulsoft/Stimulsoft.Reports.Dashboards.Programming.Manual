# Viewer Events

The report viewer supports events that provide the ability to perform necessary operations before specific actions—both on the JavaScript client side and the Python server side. A detailed description of how events work can be found in the [Report Engine Events section](../Engine/Events.md).

Some event arguments take values from enumerations that are located in specific namespaces. All the enumerations used in designer events are listed in the code block below:


**app.py**

```python

from stimulsoft_reports.enums import StiEventType
from stimulsoft_reports.report.enums import StiExportFormat
from stimulsoft_reports.viewer.enums import StiPrintAction, StiExportAction
```


**viewer.html**

```html

<script>
    StiExportAction = Stimulsoft.Viewer.StiExportAction;
    StiExportFormat = Stimulsoft.Report.StiExportFormat;
</script>
```

The viewer supports the following events:

- [onPrepareVariables](#onpreparevariables)
- [onBeginProcessData](#onbeginprocessdata)
- [onEndProcessData](#onendprocessdata)
- [onOpenReport](#onopenreport)
- [onOpenedReport](#onopenedreport)
- [onPrintReport](#onprintreport)
- [onBeginExportReport](#onbeginexportreport)
- [onEndExportReport](#onendexportreport)
- [onInteraction](#oninteraction)
- [onEmailReport](#onemailreport)
- [onDesignReport](#ondesignreport)

### onPrepareVariables

[v] JavaScript  [v] Python


The event is triggered before the report is built, after the report variables are prepared. A list of event arguments can be found in the [Report Engine Events](../Engine/Events.md) section. Detailed descriptions and usage examples can be found in the[Working with Report Variables](Work_with_Parameters.md) section.

### onBeginProcessData

[v] JavaScript  [v] Python


The event is triggered before requesting the data needed to build the report. A list of event arguments can be found in the [Report Engine Events](../Engine/Events.md) section. Detailed descriptions and usage examples can be found in the [Connecting Data Files](../Engine/Connecting_Data_Files.md) and [Connecting SQL Data Adapters](../Engine/Connecting_SQL_Data.md) sections.

### onEndProcessData

[v] JavaScript  [v] Python


The event is triggered after the data is loaded, before the report is built. A list of event arguments can be found in the "[Report Engine Events](../Engine/Events.md)" section. Detailed descriptions and usage examples can be found in the [Connecting Data Files](../Engine/Connecting_Data_Files.md) and [Connecting SQL Data Adapters](../Engine/Connecting_SQL_Data.md) sections.

**onOpenReport**
[v] JavaScript  [x] Python


The event is triggered before opening the report after the toolbar button is clicked.


List of properties passed in the event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event has the value  "`OpenReport`". |
| `sender` | The identifier of the component that initiated this event can take the following value: - `"Viewer"` - `"Designer"` |
| `report` | The current report object will be passed as `null` in the arguments of this event. |
| `preventDefault` | This flag allows you to stop further event handling by the viewer. By default, it is set to `false`. |

**onOpenedReport**
[v] JavaScript  [v] Python


The event is triggered after opening a report from the designer menu but before it is loaded into the viewer.


List of properties passed in the event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, with the value  "`OpenedReport`". |
| `sender` | The identifier of the component that initiated the event, which can have the following value: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `preventDefault` | This flag allows you to stop further event processing by the designer. By default, it is set to `false`. |

List of properties passed in the event arguments on the Python server side. The arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, for this event the value is  `StiEventType.OPENED_REPORT` |
| `sender` | The identifier of the component that initiated the event, which can take the following value: - `StiViewer` - `StiDesigner` |
| `report` | The current report object in the form of a JSON string or object. |

### onPrintReport

[v] JavaScript  [v] Python


The event is triggered before printing the report. The table below shows the list of event handler arguments on the client-side in JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, with the value  "`PrintReport`". |
| `sender` | The identifier of the component that triggered this event, possible values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `printAction` | The type of report printing. Possible values: - `PrintPdf` - prints in PDF format; - `PrintWithoutPreview` - prints in HTML format directly to the printer,  displays the system print dialog; - `PrintWithPreview` - prints in HTML format with a preview in a popup. |
| `preventDefault` | This flag allows you to stop further event handling by the viewer. By default, it is set to `false`. |

The list of properties passed as event arguments on the server side in Python has the type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the  `StiEventType.PRINT_REPORT`. |
| `sender` | The identifier of the component that triggered this event, possible values: - `StiViewer` - `StiDesigner` |
| `report` | The current report object. |
| `printAction` | The type of report printing. Possible values: - `StiPrintAction.PRINT_PDF` - prints in PDF format; - `StiPrintAction.PRINT_WITHOUT_PREVIEW` - prints in HTML format directly  to the printer, displays the system print dialog; - `StiPrintAction.PRINT_WITH_PREVIEW` - prints in HTML format with a preview in a popup. |

For detailed descriptions and usage examples, refer to the [Report Printing](Printing_Report.md) section.

### onBeginExportReport

[v] JavaScript  [v] Python


The event is triggered before exporting the report, after the export settings dialog. The table below shows the list of event handler arguments on the client-side in JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value "`BeginExportReport`". |
| `sender` | The identifier of the component that triggered this event, possible values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `action` | The action that triggered the export event, possible values: - `StiExportAction.ExportReport` - `StiExportAction.SendEmail` |
| `format` | The selected report export format, possible values: - `StiExportFormat.Document` - `StiExportFormat.Pdf` - `StiExportFormat.Xps` - `StiExportFormat.Ppt2007` - `StiExportFormat.Html` - `StiExportFormat.Html5` - `StiExportFormat.Text` - `StiExportFormat.Word2007` - `StiExportFormat.Excel2007` - `StiExportFormat.Odt` - `StiExportFormat.Ods` - `StiExportFormat.Csv` - `StiExportFormat.ImageSvg` |
| `formatName` | The name of the selected export format, corresponds to the format enumeration constants. |
| `settings` | The settings of the selected export format. The available properties list will depend on the chosen export type. |
| `fileName` | The report file name to save after export completion. |
| `openAfterExport` | A flag indicating whether the report will be exported in a new browser tab (``true``), or if the file save dialog will be prompted after the export (``false``). |
| `preventDefault` | This flag allows you to stop further event handling by the viewer. By default, it is set to `false`. |

The list of properties passed as event arguments on the server side in Python has the type  `StiExportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value  `StiEventType.BEGIN_EXPORT_REPORT`. |
| `sender` | The identifier of the component that triggered this event, possible values: - `StiViewer` - `StiDesigner` |
| `report` | The current report object. |
| `action` | The action that triggered the export event, possible values: - `StiExportAction.EXPORT_REPORT` - `StiExportAction.SEND_EMAIL` |
| `format` | The selected report export format, possible values: - `StiExportFormat.DOCUMENT` - `StiExportFormat.PDF` - `StiExportFormat.XPS` - `StiExportFormat.PPT2007` - `StiExportFormat.HTML` - `StiExportFormat.HTML5` - `StiExportFormat.TEXT` - `StiExportFormat.WORD2007` - `StiExportFormat.EXCEL2007` - `StiExportFormat.ODT` - `StiExportFormat.ODS` - `StiExportFormat.CSV` - `StiExportFormat.IMAGE_SVG` |
| `formatName` | The name of the selected export format, corresponds to the format enumeration constants. |
| `settings` | The settings of the selected export format. The available properties list will depend on the chosen export type. |
| `fileName` | The report file name to save after export completion. |
| `openAfterExport` | A flag indicating whether the report will be exported in a new browser tab (``true``), or if the file save dialog will be prompted after the export (``false``). |

### onEndExportReport

[v] JavaScript  [v] Python


The event is triggered after the report has been exported, but before it is saved as a file. The table below shows the list of event handler arguments on the client-side in JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value  "`EndExportReport`". |
| `sender` | The identifier of the component that triggered this event, possible values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `format` | The selected report export format, possible values: - `StiExportFormat.Document` - `StiExportFormat.Pdf` - `StiExportFormat.Xps` - `StiExportFormat.Ppt2007` - `StiExportFormat.Html` - `StiExportFormat.Html5` - `StiExportFormat.Text` - `StiExportFormat.Word2007` - `StiExportFormat.Excel2007` - `StiExportFormat.Odt` - `StiExportFormat.Ods` - `StiExportFormat.Csv` - `StiExportFormat.ImageSvg` |
| `formatName` | The name of the selected export format, corresponds to the format enumeration constants. |
| `data` | The byte data of the exported report, prepared for saving to a file. |
| `fileName` | The report file name to save after export completion. |
| `openAfterExport` | A flag indicating whether the report will be exported in a new browser tab (``true``), or if the file save dialog will be prompted after the export (``false``). |
| `preventDefault` | This flag allows you to stop further event handling by the viewer. By default, it is set to `false`. |

The list of properties passed as event arguments on the server side in Python has the type  `StiExportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value  `StiEventType.END_EXPORT_REPORT`. |
| `sender` | The identifier of the component that triggered this event, possible values: - `StiViewer` - `StiDesigner` |
| `format` | The selected report export format, possible values: - `StiExportFormat.DOCUMENT` - `StiExportFormat.PDF` - `StiExportFormat.XPS` - `StiExportFormat.PPT2007` - `StiExportFormat.HTML` - `StiExportFormat.HTML5` - `StiExportFormat.TEXT` - `StiExportFormat.WORD2007` - `StiExportFormat.EXCEL2007` - `StiExportFormat.ODT` - `StiExportFormat.ODS` - `StiExportFormat.CSV` - `StiExportFormat.IMAGE_SVG` |
| `formatName` | The name of the selected export format, corresponds to the format enumeration constants. |
| `data` | The byte data of the exported report, prepared for saving to a file. |
| `fileName` | The report file name to save after export completion. |
| `fileExtension` | The file extension for the report to save after export completion, corresponds to the selected format type. |
| `mimeType` | The MIME type for the selected export format. |
| `openAfterExport` | A flag indicating whether the report will be exported in a new browser tab (``true``), or if the file save dialog will be prompted after the export (``false``). |

### onInteraction

[v] JavaScript  [x] Python


The event is triggered at the moment of an interactive action in the viewer (dynamic sorting, collapsing, drill-down, applying parameters) before the report generator processes the values. The table below shows the list of event handler arguments on the client-side in JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value  "`Interaction`". |
| `sender` | The identifier of the component that triggered this event, possible values: - "`Viewer`" - "`Designer`" |
| `report` | The current report object. |
| `action` | The identifier of the current interactive action, possible values: - "`InitVars`" - triggered when initializing report variables requested from the user; - "`Variables`" - triggered when applying the values of variables requested from the user; - "`Sorting`" - triggered when sorting columns; - "`DrillDown`" - triggered during report drill-down; - "`Collapsing`" - triggered when collapsing report sections; - "`DashboardFiltering`" - triggered when using filters within a dashboard element; - "`DashboardSorting`" - triggered when sorting within a dashboard element; - "`DashboardResetAllFilters`" - triggered when resetting all sorting and filters in a dashboard element to the values defined in the template; - "`DashboardElementDrillDown`" - triggered during drill-down of a dashboard element; - "`DashboardElementDrillUp`" - triggered during drill-up of a dashboard element; |
| `variables` | A collection of report variables and their values, set on the parameters panel.. |
| `sortingParameters` | A collection of parameters required for dynamic report sorting. |
| `collapsingParameters` | A collection of parameters required for dynamic collapsing of report elements. |
| `drillDownParameters` | A collection of parameters required for report drill-down. |
| `filteringParameters` | A collection of parameters required for sorting, filtering, and drill-down in dashboard elements. |
| `preventDefault` | This flag allows stopping further event handling. By default, it is set to `false`. |

### onEmailReport

[v] JavaScript  [v] Python


The event is triggered after the report is exported and before it is sent via Email. The table below lists the event handler arguments on the client side in JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value  "`EmailReport`". |
| `sender` | The identifier of the component that triggered this event, possible values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `format` | The selected report export format, possible values: - `StiExportFormat.Document` - `StiExportFormat.Pdf` - `StiExportFormat.Xps` - `StiExportFormat.Ppt2007` - `StiExportFormat.Html` - `StiExportFormat.Html5` - `StiExportFormat.Text` - `StiExportFormat.Word2007` - `StiExportFormat.Excel2007` - `StiExportFormat.Odt` - `StiExportFormat.Ods` - `StiExportFormat.Csv` - `StiExportFormat.ImageSvg` |
| `formatName` | The name of the selected report export format, corresponding to the format enum constants. |
| `data` | The byte data of the exported report, prepared for sending via Email. |
| `fileName` | The name of the report file for sending by Email. |
| `settings` | An object containing the parameters filled in the viewer's Email sending dialog. |

The table below shows the list of Email sending parameters on the client-side in JavaScript.


| **Name** | **Description** |
| --- | --- |
| `settings.email` | The Email address to which the exported report will be sent. |
| `settings.subject` | The subject of the email. |
| `settings.message` | The text of the email. |

List of properties passed in the event arguments on the Python server-side. The arguments are of type `StiExportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, for this event it is  `StiEventType.EMAIL_REPORT`. |
| `sender` | The identifier of the component that triggered this event, possible values: - `StiViewer` - `StiDesigner` |
| `report` | The current report object in JSON format. |
| `format` | The selected report export format, possible values: - `StiExportFormat.DOCUMENT` - `StiExportFormat.PDF` - `StiExportFormat.XPS` - `StiExportFormat.PPT2007` - `StiExportFormat.HTML` - `StiExportFormat.HTML5` - `StiExportFormat.TEXT` - `StiExportFormat.WORD2007` - `StiExportFormat.EXCEL2007` - `StiExportFormat.ODT` - `StiExportFormat.ODS` - `StiExportFormat.CSV` - `StiExportFormat.IMAGE_SVG` |
| `formatName` | The name of the selected report export format, matching the enum constants. |
| `data` | The byte data of the exported report, prepared for sending via Email. |
| `fileName` | The name of the report file for sending by Email. |
| `settings` | An object containing the Email sending parameters on the server-side. |

List of Email sending parameters on the Python server-side. All settings are in the `StiEmailSettings` class:


| **Name** | **Description** |
| --- | --- |
| `fromAddr` | The email address of the sender. |
| `name` | The full name of the sender. |
| `toAddr` | The email address to which the exported report will be sent (from the viewer's dialog). |
| `subject` | The email subject (from the viewer's dialog). |
| `message` | The email text (from the viewer's dialog). |
| `attachmentName` | The name of the report file in the attachment (default: report file name). |
| `charset` | The character encoding used for the email body (default: "UTF-8"). |
| `host` | The SMTP server address (required). |
| `port` | The SMTP server port (default: 465). |
| `login` | The login for the email server (required). |
| `password` | The password for the email server (required). |
| `secure` | The type of encryption for the email connection (`ssl` or tls, default: `ssl`). |
| `cc` | An array of CC (Carbon Copy) addresses for secondary recipients. |
| `bcc` | An array of BCC (Blind Carbon Copy) addresses for hidden recipients. |

### onDesignReport

[v] JavaScript  [x] Python


The event is triggered when the Design button on the viewer panel is clicked. The table below lists the event handler arguments on the client side in JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, with the value  "`DesignReport`". |
| `sender` | The identifier of the component that triggered the event, possible value: - `"Viewer"` |
| `report` | The current report object. |
| `fileName` | The name of the report file to be passed and loaded into the designer. |
