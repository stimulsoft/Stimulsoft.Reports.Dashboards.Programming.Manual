# Viewer Events

The report viewer supports events that allow executing necessary operations before certain actions, both on the client JavaScript side and the server PHP side. Detailed descriptions of event handling can be found in the [Report Engine Events](../Engine/Events.md) section.


The viewer supports the following events:

- [onDatabaseConnect](#ondatabaseconnect)

- [onBeginProcessData](#onbeginprocessdata)
- [onEndProcessData](#onendprocessdata)
- [onPrepareVariables](#onpreparevariables)
- [onOpenReport](#onopenreport)
- [onOpenedReport](#onopenedreport)
- [onPrintReport](#onprintreport)
- [onBeginExportReport](#onbeginexportreport)
- [onEndExportReport](#onendexportreport)
- [onInteraction](#oninteraction)
- [onEmailReport](#onemailreport)
- [onDesignReport](#ondesignreport)

### onDatabaseConnect

[-] JavaScript  [+] PHP


This event is triggered before connecting to the database after receiving all the parameters. Detailed descriptions and usage examples can be found in the [Connetting SQL Data Adapter](../Engine/Connecting_SQL_Data.md) section. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.

### onBeginProcessData

[+] JavaScript  [+] PHP


This event is triggered before requesting the data needed to generate the report. Detailed descriptions and usage examples can be found in the [Connecting Data](../Engine/Connecting_Data_Files.md) and[Connetting SQL Data Adapter](../Engine/Connecting_SQL_Data.md) sections. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.


### onEndProcessData

[+] JavaScript  [+] PHP


This event is triggered before requesting the data needed to generate the report. Detailed descriptions and usage examples can be found in the [Connecting Data](../Engine/Connecting_Data_Files.md) and[Connetting SQL Data Adapter](../Engine/Connecting_SQL_Data.md) sections. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.


### onPrepareVariables

[+] JavaScript  [+] PHP


This event is triggered before generating the report, after preparing the report variables. Detailed descriptions and usage examples can be found in the [Working with Report Variables](../Engine/Using_Variables.md) section. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.

### onOpenReport

[+] JavaScript  [-] PHP


This event is triggered before opening a report after clicking the toolbar button. The table below contains a list of properties passed as event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`OpenReport`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - "`Viewer`" - "`Designer`" |
| `report` | The current report object. The value passed in the event arguments will be `null`. |
| `preventDefault` | This flag allows you to stop further processing of the event by the viewer. The default value is `false`. |

**onOpenedReport**

[+] JavaScript  [+] PHP


This event is triggered after the report file is opened but before it is sent to the viewer. The table below contains a list of properties passed as event arguments on the JavaScript client-side.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`OpenedReport`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - "`Viewer`" - "`Designer`" |
| `report` | The current report object. |
| `preventDefault` | This flag allows you to stop further processing of the event by the viewer. The default value is`false`. |

The table below contains a list of properties passed as event arguments on the JavaScript client-side and on the PHP server-side, arguments are of the `StiReportEventArgs` type.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier for this event is `StiEventType::OpenedReport`. |
| `sender` | The component that triggered this event can have the following types: - `StiViewer` - `StiDesigner` |
| `report` | The current report object. |

### onPrintReport

[+] JavaScript  [+] PHP


This event is triggered before printing the report. Detailed descriptions and usage examples can be found in the [Report Printing](Printing_Report.md) section.


The table below contains a list of properties passed as event arguments on the JavaScript client-side.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`PrintReport`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `printAction` | Report print type can take the following values: - `"PrintPdf"` - print in PDF format; - `"PrintWithoutPreview"` - print in HTML format directly to the printer, displaying the system print dialog; - `"PrintWithPreview"` - print in HTML format directly to the printer, displaying the system print dialog; |
| `pageRange` | The object containing the page range settings for printing. |
| `preventDefault` | This flag allows you to stop further processing of the event by the viewer. The default value is `false`. |

A list of event arguments is available for both JavaScript client-side and PHP server-side, `StiPrintEventArgs` type.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier for this event is `StiEventType::PrintReport`. |
| `sender` | The component that triggered this event can have the following types: - `StiViewer` - `StiDesigner` |
| `report` | The current report object. |
| `printAction` | Report print type can take the following values: - `StiPrintAction::PrintPdf` - print in PDF format; - `StiPrintAction::PrintWithoutPreview` - print in HTML format directly to the printer, displaying the system print dialog; - `StiPrintAction::PrintWithPreview` - print in HTML format with a preview in a pop-up window. |
| `fileName` | The report file name for saving. |
| `pageRange` | The object containing the page range settings for printing. |

### onBeginExportReport

[+] JavaScript  [+] PHP


This event is triggered before exporting the report, right after the export settings dialog. Detailed descriptions and usage examples can be found in the [Report Export](Export.md) section.


The table below contains a list of properties passed as event arguments on the JavaScript client-side.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`BeginExportReport`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `action` | The action that triggered the export event can take the following following values `Stimulsoft.Viewer.StiExportAction`: - `StiExportAction.ExportReport` - `StiExportAction.SendEmail` |
| `format` | The selected report export format. Can take the following enumeration values `Stimulsoft.Report.StiExportFormat`: - `StiExportFormat.Document` - `StiExportFormat.Pdf` - `StiExportFormat.Xps` - `StiExportFormat.PowerPoint` - `StiExportFormat.Html` - `StiExportFormat.Html5` - `StiExportFormat.Text` - `StiExportFormat.Word` - `StiExportFormat.Excel` - `StiExportFormat.Odt` - `StiExportFormat.Ods` - `StiExportFormat.Rtf` - `StiExportFormat.Csv` - `StiExportFormat.Json` - `StiExportFormat.Xml` - `StiExportFormat.Dbf` - `StiExportFormat.Sylk` - `StiExportFormat.ImagePng` - `StiExportFormat.ImageJpeg` - `StiExportFormat.ImageGif` - `StiExportFormat.ImageTiff` - `StiExportFormat.ImageSvg` - `StiExportFormat.ImageSvgz` - `StiExportFormat.ImagePcx` - `StiExportFormat.ImageBmp` |
| `formatName` | The name of the selected export format matches the constant names in the export format enumeration. |
| `settings` | Settings for the selected export format. The type of the settings object and the list of available properties will depend on the selected export type. |
| `fileName` | The report file name for saving after the export is completed. |
| `openAfterExport` | This flag allows enabling automatic opening of the exported report in a new browser tab instead of saving it to a file. It works only for formats supported by the browser. The default value is `false`. |
| `preventDefault` | This flag allows stopping further processing of the event by the viewer. The default value is `false`. |

A list of event arguments is available for both JavaScript client-side and PHP server-side `StiExportEventArgs` type:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value `StiEventType::BeginExportReport`. |
| `sender` | The component that triggered this event can be of the following types: - `StiViewer` - `StiDesigner` |
| `action` | The action that triggered the export event can take the following values: - `StiExportAction::ExportReport` - `StiExportAction::SendEmail` |
| `format` | The selected export format can take the following values: - `StiExportFormat::Document` - `StiExportFormat::Pdf` - `StiExportFormat::Xps` - `StiExportFormat::PowerPoint` - `StiExportFormat::Html` - `StiExportFormat::Html5` - `StiExportFormat::Text` - `StiExportFormat::Word` - `StiExportFormat::Excel2007` - `StiExportFormat::Odt` - `StiExportFormat::Ods` - `StiExportFormat::Rtf` - `StiExportFormat::Csv` - `StiExportFormat::Json` - `StiExportFormat::Xml` - `StiExportFormat::Dbf` - `StiExportFormat::Sylk` - `StiExportFormat::ImagePng` - `StiExportFormat::ImageJpeg` - `StiExportFormat::ImageGif` - `StiExportFormat::ImageTiff` - `StiExportFormat::ImageSvg` - `StiExportFormat::ImageSvgz` - `StiExportFormat::ImagePcx` - `StiExportFormat::ImageBmp` |
| `formatName` | The name of the selected export format corresponds to the constant names in the export format enumeration. |
| `fileName` | The report file name for saving after the export is completed. |
| `settings` | Settings for the selected export format. The type of settings object and the list of available properties will depend on the selected export type. |
| `openAfterExport` | This flag allows enabling automatic opening of the exported report in a new browser tab instead of saving it to a file. It works only for formats supported by the browser. The default value is `false`. |

### onEndExportReport

[+] JavaScript  [+] PHP


This event is triggered after exporting the report but before saving it as a file. Detailed descriptions and usage examples can be found in the [Report Export](Export.md) section.


The table below contains a list of properties passed as event arguments on the JavaScript client-side.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`EndExportReport`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `format` | The selected export format can take the following values - `StiExportFormat.Document` - `StiExportFormat.Pdf` - `StiExportFormat.Xps` - `StiExportFormat.PowerPoint` - `StiExportFormat.Html` - `StiExportFormat.Html5` - `StiExportFormat.Text` - `StiExportFormat.Word` - `StiExportFormat.Excel` - `StiExportFormat.Odt` - `StiExportFormat.Ods` - `StiExportFormat.Rtf` - `StiExportFormat.Csv` - `StiExportFormat.Json` - `StiExportFormat.Xml` - `StiExportFormat.Dbf` - `StiExportFormat.Sylk` - `StiExportFormat.ImagePng` - `StiExportFormat.ImageJpeg` - `StiExportFormat.ImageGif` - `StiExportFormat.ImageTiff` - `StiExportFormat.ImageSvg` - `StiExportFormat.ImageSvgz` - `StiExportFormat.ImagePcx` - `·StiExportFormat.ImageBmp` |
| `formatName` | The name of the selected export format corresponds to the constant names in the export format enumeration. |
| `data` | Byte data of the exported report prepared for saving to a file. |
| `fileName` | The report file name for saving after the export is completed. |
| `openAfterExport` | This flag allows enabling automatic opening of the exported report in a new browser tab instead of saving it to a file. It works only for formats supported by the browser. The default value is `false`. |
| `preventDefault` | This flag allows stopping further processing of the event by the viewer. The default value is `false`. |

A list of event arguments is available for both JavaScript client-side and PHP server-side `StiExportEventArgs` type:


| **Name** | **Description** |
| --- | --- |
|  | Current event identifier, has the value `StiEventType::EndExportReport`. |
| `sender` | The identifier of the component that triggered this event can take the following values: - `StiViewer` - `StiDesigner` |
| `format` | The selected export format can take the following values from the Stimulsoft.Report.StiExportFormat enumeration: - `StiExportFormat::Document` - `StiExportFormat::Pdf` - `StiExportFormat::Xps` - `StiExportFormat::PowerPoint` - `StiExportFormat::Html` - `StiExportFormat::Html5` - `StiExportFormat::Text` - `StiExportFormat::Word` - `StiExportFormat::Excel2007` - `StiExportFormat::Odt` - `StiExportFormat::Ods` - `StiExportFormat::Rtf` - `StiExportFormat::Csv` - `StiExportFormat::Json` - `StiExportFormat::Xml` - `StiExportFormat::Dbf` - `StiExportFormat::Sylk` - `StiExportFormat::ImagePng` - `StiExportFormat::ImageJpeg` - `StiExportFormat::ImageGif` - `StiExportFormat::ImageTiff` - `StiExportFormat::ImageSvg` - `StiExportFormat::ImageSvgz` - `StiExportFormat::ImagePcx` - `StiExportFormat::ImageBmp` |
| `formatName` | The name of the selected export format corresponds to the constant names in the format enumeration. |
| `data` | The byte data of the exported report, prepared for saving to a file, is in `Base64` format. |
| `fileName` | The report file name for saving after the export is completed. |
| `fileExtension` | The file extension for the report corresponds to the selected export format. |
| `mimeType` | The MIME type for the selected export format. |
| `openAfterExport` | This flag allows enabling automatic opening of the exported report in a new browser tab instead of saving it to a file. It works only for formats supported by the browser. The default value is `false`. |

### onInteraction

[+] JavaScript  [-] PHP


This event is triggered during any interactive action in the viewer (such as dynamic sorting, collapsing, drilling down, or applying parameters) before the values are processed by the report generator. Detailed descriptions and usage examples can be found in the [Dynamic Sorting, Collapsing, and Drilling Down](Interaction.md) section.


The table below contains a list of properties passed as event arguments on the JavaScript client-side.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`Interaction`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `action` | The identifier of the current interactive action can take the following values: - `"InitVars"` - the action occurs during the initialization of report variables requested from the user; - `"Variables"` - the action occurs when applying values of variables requested from the user; - `"Sorting"` - the action occurs when using column sorting; - `"DrillDown"` - the action occurs during report drill-down; - `"Collapsing"` - the action occurs when collapsing report blocks; - `"DashboardFiltering"` - the action occurs when using filters within a dashboard element; - `"DashboardSorting"` - the action occurs when using sorting within a dashboard element; - `"DashboardResetAllFilters"` - the action occurs when resetting sorting and filters within a dashboard element to the values set in the template; - `"DashboardElementDrillDown"` - the action occurs when using drill-down within a dashboard element; - `"DashboardElementDrillUp"` - the action occurs when using drill-up within a dashboard element. |
| `variables` | The collection of report variables and their values set on the parameter panel. |
| `sortingParameters` | The collection of parameters necessary for dynamic sorting of the report. |
| `collapsingParameters` | The collection of parameters necessary for dynamically collapsing report elements. |
| `drillDownParameters` | The collection of parameters necessary for report drill-down. |
| `filteringParameters` | The collection of parameters necessary for sorting, filtering, and drill-down of dashboard elements. |
| `preventDefault` | This flag allows stopping further event processing. The default value is `false`. |

### onEmailReport

[+] JavaScript  [+] PHP


The event is triggered after the report is exported, before it is sent by Email. Detailed descriptions and usage examples can be found in the [Sending Report by Email](Send_Email.md) section.


The table below contains a list of properties passed as event arguments on the JavaScript client-side.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`EmailReport`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - `"Viewer"` - `"Designer"` |
| `report` | The current report object. |
| `format` | The selected export format of the report can take the following values from the  `Stimulsoft.Report.StiExportFormat` enumeration: - `StiExportFormat.Document` - `StiExportFormat.Pdf` - `StiExportFormat.Xps` - `StiExportFormat.PowerPoint` - `StiExportFormat.Html` - `StiExportFormat.Html5` - `StiExportFormat.Text` - `StiExportFormat.Word` - `StiExportFormat.Excel` - `StiExportFormat.Odt` - `StiExportFormat.Ods` - `StiExportFormat.Rtf` - `StiExportFormat.Csv` - `StiExportFormat.Json` - `StiExportFormat.Xml` - `StiExportFormat.Dbf` - `StiExportFormat.Sylk` - `StiExportFormat.ImagePng` - `StiExportFormat.ImageJpeg` - `StiExportFormat.ImageGif` - `StiExportFormat.ImageTiff` - `StiExportFormat.ImageSvg` - `StiExportFormat.ImageSvgz` - `StiExportFormat.ImagePcx` - `·StiExportFormat.ImageBmp` |
| `formatName` | The name of the selected export format corresponds to the constant names in the export format enumeration. |
| `data` | Byte data of the exported report prepared for sending by email. |
| `fileName` | The report file name for sending by email. |
| `settings` | An object containing the parameters filled out in the viewer's email sending dialog. A description of all parameters is provided in a separate table below. |

The table below lists the Email sending parameters on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `email` | The email address to which the exported report will be sent. |
| `subject` | The subject of the email. |
| `message` | The message text of the email. |

A list of event arguments is available for both JavaScript client-side and PHP server-side `StiEmailEventArgs`type:


| **Name** | **Description** |
| --- | --- |
|  | Current event identifier, has the value `StiEventType::EmailReport.` |
| `sender` | The identifier of the component that triggered this event can take the following values: - `StiViewer` - `StiDesigner` |
| `format` | The selected export format can take the following values: - `StiExportFormat::Document` - `StiExportFormat::Pdf` - `StiExportFormat::Xps` - `StiExportFormat::PowerPoint` - `StiExportFormat::Html` - `StiExportFormat::Html5` - `StiExportFormat::Text` - `StiExportFormat::Word` - `StiExportFormat::Excel2007` - `StiExportFormat::Odt` - `StiExportFormat::Ods` - `StiExportFormat::Rtf` - `StiExportFormat::Csv` - `StiExportFormat::Json` - `StiExportFormat::Xml` - `StiExportFormat::Dbf` - `StiExportFormat::Sylk` - `StiExportFormat::ImagePng` - `StiExportFormat::ImageJpeg` - `StiExportFormat::ImageGif` - `StiExportFormat::ImageTiff` - `StiExportFormat::ImageSvg` - `StiExportFormat::ImageSvgz` - `StiExportFormat::ImagePcx` - `StiExportFormat::ImageBmp` |
| `formatName` | The name of the selected export format corresponds to the constant names in the format enumeration. |
| `data` | The byte data of the exported report, prepared for sending by Email, is in `Base64` format. |
| `fileName` | The report file name for sending by Email. |
| `settings` | An object containing the Email sending parameters on the server-side. A detailed description of all parameters is provided in a separate table below. |

A list of event arguments is available for both JavaScript client-side and PHP server-side `StiEmailSettings` type:


| **Name** | **Description** |
| --- | --- |
| `from` | The sender's Email address. |
| `name` | The sender's first and last name. |
| `to` | The recipient's Email address to which the exported report will be sent, provided from the viewer dialog. |
| `subject` | The subject of the Email, provided from the viewer dialog. |
| `message` | The mesage of the Email, provided from the viewer dialog. |
| `attachmentName` | The report file name in the attachment, by default, the report file name is used. |
| `charset` | The character encoding used for the Email body, "UTF-8" is used by default. |
| `host` | The SMTP server address. This is a required field. |
| `port` | The SMTP server port, 465 is used by default. |
| `secure` | The type of encryption for the connection with the mail server, either "`ssl`" (default) or "`tls`" encryption can be used. |
| `login` | The login for connecting to the mail server. This is a required field. |
| `password` | The password for connecting to the mail server. This is a required field. |
| `cc` | An array of CC (Carbon Copy) addresses for secondary Email recipients. |
| `bcc` | An array of BCC (Blind Carbon Copy) addresses for hidden Email recipients. |

### onDesignReport

[+] JavaScript  [-] PHP


This event is triggered when clicking the Design button on the viewer's toolbar. Detailed descriptions and usage examples can be found in the [Call the Designer](Call_Designer.md) from the Viewer section.


The table below contains a list of properties passed as event arguments on the JavaScript client-side.


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`DesignReport`". |
| `sender` | The identifier of the component that triggered this event can take the following values: - `"Viewer"` |
| `report` | The current report object. |
| `fileName` | The current report file name. |
