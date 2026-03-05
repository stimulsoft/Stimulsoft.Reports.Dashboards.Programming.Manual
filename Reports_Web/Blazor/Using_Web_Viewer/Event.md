# Viewer Events

The **Blazor Viewer** component supports events which allows you to execute necessary operations before certain actions, such as printing and exporting, sending reports by email, interactivity etc. Below is a sample of processing viewer events.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer OnViewerReport="@OnViewerEvent" />

@code
{
    private void OnViewerEvent(StiReportDataEventArgs args)
    {
        var action = args.Action;
        var report = args.Report;
        var parameters = args.RequestParams;
    }
}
```

### Events list


| **Name** | **Description** |
| --- | --- |
| OnOpenReport | The event occurs when [opening a report](Showing_Reports.md). |
| OnPrintReport | The event occurs when [printing a report](Printing_Reports.md). |
| OnExportReport | The event occurs when [exporting a report](Export.md). |
| OnEmailReport | The event occurs when [sending a report by email](Send_Email.md). |
| OnInteraction | The event occurs when the viewer works with interactive operations, such as [using parameters](Work_with_Parameters.md), [dynamic sorting, collapsing, and drilling a report](Interaction.md). |
| OnViewerEvents | The event occurs for any action in the report viewer. |
| OnDesignReport | The event occurs when [pressing the Design button](Call_Designer.md) on the toolbar of the viewer. |
| OnViewerAfterRender | The event occurs when the HTML5 code of the viewer and all its controls have been completed. |
