## Export Service

The way to create the export service is shown below. See the code:


**C#**

```csharp
...
StiPdfExportService service = new StiPdfExportService();
StiPdfExportSettings settings = new StiPdfExportSettings();
MemoryStream stream = new MemoryStream();
service.ExportPdf(report, stream, settings);
...
```

If you exported from the WinForms Viewer, then you should notice, than for each export the special form for setting parameters of export is shown. This form can be called from the code. The code below how to do it for the export to the **PDF**:


**C#**

```csharp
...
service.Export(report, "MyReport.pdf");
...
```

This code will call the dialog form for setting parameters of export. If a user clicks "OK", then the file will be created. If to click the "Cancel" button, then the file creation will be interrupted.


> **Information**
>
> The name of the method for the report export with dialog forms differs from the name of the export method without parameters.

The export service of a report contains yet another ability. The report can be sent via Email. For example:


**C#**

```csharp
...
bool sendEMail = true;
service.Export(report, "MyReport.pdf", sendEMail);
...
```

This code will call the dialog form for setting parameters of reports, and if a user clicks "OK", then the reporting tool will call the Email client and will create a new Email Email, the exported report will be attached to the Email Email. The code above requires connection of the following names from the **Stimulsoft.Report.dll** assemblies:


**C#**

```csharp
...
Stimulsoft.Report
Stimulsoft.Report.Export
...
```

### All Export Services

The **StiExportFormat** enumeration describes export formats. Brief information of exports is represented below.


| **Export services to Adobe PDF and Microsoft XPS:** StiPdfExportService, StiXpsExportService | **Export services to HTML and MHT:** StiHtmlExportService StiMhtExportService |
| --- | --- |
| **Export services to text formats:** StiTxtExportService StiRtfExportService StiWord2007ExportService StiOdtExportService | **Export services to Microsoft Excel and Open Document Calc:** StiExcelXmlExportService StiExcelExportService StiExcel2007ExportService StiOdsExportService |
| **Export services to graphic formats:** StiBmpExportService StiGifExportService StiJpegExportService StiPcxExportService StiPngExportService StiTiffExportService StiEmfExportService | **Export services to data:** StiCsvExportService StiDbfExportService StiXmlExportService StiDifExportService StiSylkExportService |
