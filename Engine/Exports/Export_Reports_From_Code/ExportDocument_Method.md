## ExportDocument Method

The **ExportDocument** method is a simplified wrapping for report exports. There is no need to get the required export service. All you need is to define the export type, pass parameters of export and define the folder where the file should be saved. For example:


**C#**

```csharp
...
StiPdfExportSettings pdfSettings = new StiPdfExportSettings();
report.ExportDocument(StiExportFormat.Pdf, "MyReport.Pdf", pdfSettings); 
...
```

The following code id used to export reports to PDF. The PDF file will be placed in the MyReport.Pdf. The export parameters can be passed using the **StiPdfExportSettings** object type. This class is described in the description of the PDF format. If there is no need to change export parameters then it is possible to use the short code line:


**C#**

```csharp
...
report.ExportDocument(StiExportFormat.Pdf, "MyReport.Pdf");
...
```

In this case the export parameters are  not passed and the report generator will use parameters which are set by default for each export. Besides, the result of export can be placed in the stream. For example:


**C#**

```csharp
...
MemoryStream stream = new MemoryStream();
report.ExportDocument(StiExportFormat.Pdf, stream);
...
```


> **Information**
>
> The **ExportDocument** method does not call the Render method automatically. Before calling the **ExportDocument** method it is necessary to render a report or load a previously rendered report.

As you can see, no services in examples were not created and samples contain simple code. All work by creating services and checking parameters can be done using the **ExportDocument** method.


The code above requires connection the following namespaces from assemblies **Stimulsoft.Reports.dll**:


**C#**

```csharp
...
Stimulsoft.Report
...
```
