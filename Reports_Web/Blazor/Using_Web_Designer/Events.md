# Designer Events

**The** **Blazor Designer** component supports events which allows you to execute necessary operations before certain actions, such as creating and editing report templates, previewing, printing and exporting, interactivity and etc. Below is a sample for processing designer events.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorDesigner Report="@Report" OnPreviewReport="@OnPreviewReport"/>

@code
{
    //Report object to use in designer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Create empty report object
        var report = new StiReport();
        
        //Load report template
        report.Load("Reports/TwoSimpleLists.mrt");
        
        //Assing report object to designer
        Report = report;
    }
    
    private void OnPreviewReport(StiReportDataEventArgs args)
    {
        //Load new data from XML file
        var data = new System.Data.DataSet();
        data.ReadXml("Data/Demo1.xml");
        
        args.Report.RegData(data);
    }
}
```

### Events list

| **Name** | **Description** |
| --- | --- |
| OnCreateReport | Occurs when [creating new reports](Creating_Report.md) from the designer menu. |
| OnOpenReport | The event occurs when you open a report from the designer menu. In the arguments of the event, the downloaded report will be sent. |
| OnPreviewReport | Occurs when [going to the preview tab](Preview.md), as well as when interactive activities such as using report variables, dynamic collapsing, drill-down, and sorting a report when previewing it. |
| OnSaveReport | Occurs when [clicking the Save button](Save_Report.md) on the panel or from the main menu of the designer. |
| OnSaveReportAs | Occurs when [clicking the Save As button](Save_Report.md) from the main menu of the designer. If the event is not specified, the report will be saved to the local disk. |
| OnExportReport | Occurs when [expoting reports](Additional_Functionality_of_Preview.md). |
| **On**DesignerEvent | The event occurs for any action in the report designer. |
| **OnPrintReport** | The event occurs when printing a report from the preview. |
| **OnExit** | The event occurs when clicking the **Exit** button in the main menu of the designer. |
| **OnDesignerAfterRender** | The event occurs when the HTML5 code of the designer and all its controls have been completed. |
