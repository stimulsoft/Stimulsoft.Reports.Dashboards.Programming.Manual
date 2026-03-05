# Viewer Events

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

**The** **HTML5 Viewer** **component supports events that allow you to execute necessary operations before specific actions, such as printing and exporting, sending reports by email, interactivity, etc. Below is a sample of processing viewer events.**


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnExportReport="StiWebViewer1_ExportReport">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_ExportReport(object sender, StiExportReportEventArgs e)
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

| **Name** | **Description** |
| --- | --- |
| OnGetReport | The event occurs when requesting a report for [preview](Showing_Reports.md). |
| OnGetReportData | The event occurs when [connecting data](Connecting_Data.md) of a report before it is rendered. |
| OnPrintReport | The event occurs when [printing reports](Printing_Reports.md). This is not relevant when viewing dashboards. |
| OnExportReport | The event occurs when [exporting reports](Export.md). |
| OnExportReportResponse | The event occurs after [exporting reports](Export.md) before saving the exported file. |
| OnEmailReport | The event occurs when [sending a report by Email](Send_Email.md). This is not relevant when viewing dashboards. |
| OnInteraction | The event occurs when interactive actions of the viewer, such as using report [variables](Work_with_Parameters.md), [dynamic collapsing, and sorting](Interaction.md). |
| OnDesignReport | The event occurs when [pressing the Design button](Call_Designer.md) on the toolbar of the viewer. |
| OnViewerEvent | The event occurs when [any action of the viewer](Main_Features.md). |
