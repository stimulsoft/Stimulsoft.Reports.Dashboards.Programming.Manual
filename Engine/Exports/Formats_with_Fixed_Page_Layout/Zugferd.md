ZUGFeRD

Stimulsoft Company has added support for the format of electronic invoices - [ZUGFeRD](https://de.wikipedia.org/wiki/ZUGFeRD).


Invoices in the **ZUGFeRD** format pass both human-readable invoices and its structured machine-readable XML based representation. Human-readable representation is encoded in the form of one or more PDF pages of the PDF/A format. XML based representation is embedded in the PDF document as an object in accordance with the specifications of the PDF/A-3 format. In other words, the invoice of the **ZUGFeRD** format contains two separate representations - human-readable in the PDF/A-3 format that is used as a container for the XML representation.


At this moment, you can use the **ZUGFeRD** format only from code. To do this, select the desired format option (V1 or V2) using the **ZUGFeRDComplianceMode** option in the export settings to PDF, using the **ZUGFeRDConformanceLevel** option, select the desired **Conformance Level**, and also load the pre-prepared XML file into the **ZUGFeRDInvoiceData** property. This will automatically add the file to the **EmbeddedFiles** collection with the standard **FileName** and **Description**. If you need to use another **Description**, you yourself can add the file to the **EmbeddedFiles** collection with the desired **FileName** and **Description**.


Pay attention:

* The name of the XML file in different versions of the standard is case-sensitive.

* ConformanceLevel COMFORT in ZUGFeRD 2.0 replaced by EN 16931.


The following is a sample code for exporting a report using the **ZUGFeRD** format:


**C#**

```csharp
...
FileStream fileStream = new FileStream(@"d:\test.pdf", FileMode.Create);
byte[] buf = File.ReadAllBytes(@"d:\ZUGFeRD-invoice.xml");

//for ZUGFeRD 1.0
var pdfExportSettings = new StiPdfExportSettings()
{
    ZUGFeRDComplianceMode = StiPdfZUGFeRDComplianceMode.V1,
    ZUGFeRDInvoiceData = buf,
    ZUGFeRDConformanceLevel = "COMFORT"    //BASIC, COMFORT, EXTENDED
};

//for ZUGFeRD 2.0
var pdfExportSettings = new StiPdfExportSettings()
{
    ZUGFeRDComplianceMode = StiPdfZUGFeRDComplianceMode.V2,
    ZUGFeRDInvoiceData = buf,
    ZUGFeRDConformanceLevel = "EN 16931"    //BASIC, EN 16931, EXTENDED
};

report.ExportDocument(StiExportFormat.Pdf, fileStream, pdfExportSettings);
fileStream.Close();
...
```

Below is an example of code for exporting a report using the **ZUGFeRD** format, if you need to use an alternative **Description** for the XML file you should to the following:


**C#**

```csharp
...
FileStream fileStream = new FileStream(@"d:\test.pdf", FileMode.Create);
byte[] buf = File.ReadAllBytes(@"d:\ZUGFeRD-invoice.xml");

//for ZUGFeRD 1.0, Custom settings
var pdfExportSettings = new StiPdfExportSettings();
pdfExportSettings.ZUGFeRDComplianceMode = StiPdfZUGFeRDComplianceMode.V1;
pdfExportSettings.EmbeddedFiles.Add(new StiPdfEmbeddedFileData("ZUGFeRD-invoice.xml", "ZUGFeRD Invoice", buf));
pdfExportSettings.ZUGFeRDConformanceLevel = "COMFORT";

//for ZUGFeRD 2.0, Custom settings
var pdfExportSettings = new StiPdfExportSettings();
pdfExportSettings.ZUGFeRDComplianceMode = StiPdfZUGFeRDComplianceMode.V2;
pdfExportSettings.EmbeddedFiles.Add(new StiPdfEmbeddedFileData("zugferd-invoice.xml", "ZUGFeRD Invoice", buf));
pdfExportSettings.ZUGFeRDConformanceLevel = "EN 16931";

report.ExportDocument(StiExportFormat.Pdf, fileStream, pdfExportSettings);
fileStream.Close();
...
```
