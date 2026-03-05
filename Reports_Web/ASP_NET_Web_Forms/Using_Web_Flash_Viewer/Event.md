# Viewer Events

**The** **Flash Viewer** component supports events which allows you to execute necessary operations before certain actions, such as printing and exporting, sending reports by email, interactivity etc. Below is a sample of processing viewer events.


**Default.aspx**

```
...
<cc1:StiWebViewerFx ID="StiWebViewerFx1" runat="server"
    OnExportReport="StiWebViewerFx1_ExportReport">
</cc1:StiWebViewerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewerFx1_ExportReport(object sender, StiExportReportEventArgs e)
{
    if (e.Format == StiExportFormat.Pdf)
    {
        StiPdfExportSettings pdfSettings = e.Settings as StiPdfExportSettings;
        pdfSettings.ImageQuality = 50;
        pdfSettings.ImageResolution = 50;
        pdfSettings.ImageCompressionMethod = StiPdfImageCompressionMethod.Jpeg;
    }
}
...
```

### List of events

**Name
              
              
                Description

                OnGetReport
              
              
                Occurs when requesting a report for preview.

                OnGetReportData
              
              
                Occurs when connecting data of a report before it is rendered.

                OnPrintReport
              
              
                Occurs when printing a report in the PDF format.

                OnExportReport
              
              
                Occurs when exporting a report.

                OnExportReportResponse
              
              
                Occurs after exporting a report before saving the exported file.

                OnEmailReport
              
              
                Occurs when sending a report by email.

                OnInteraction
              
              
                The event occurs at some interactive actions of the viewer, such as using report variables, dynamic collapsing, drill-down, and sorting in reports.

                OnDesignReport
              
              
                Occurs when clicking the Design button on the toolbar of the viewer.

                OnExit
              
              
                Occurs when clicking the Exit button on the toolbar of the viewer.**
