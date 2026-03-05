# Export and Printing from Code

The **Blazor Viewer** provides the ability to print reports in various ways and export reports to various formats. These actions are performed using the viewer menu. If you want to print or export a report by using the code, for example, in the event of pressing the button, you can use the special **StiReportResponse** class. This class contains a set of static methods that allow you to print or export a report from the code, and the report viewer is not required.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<button @onclick="@OnClickPrintButton">Print PDF</button>
<button @onclick="@OnClickExportButton">Export PDF</button>

@code
{
    private StiReport LoadSimpleList()
    {
        var dataSet = new System.Data.DataSet();
        dataSet.ReadXml("Data/Demo.xml");
        
        var report = new StiReport();
        report.Load("Reports/SimpleList.mrt");
        report.RegData(dataSet);
        
        return report;
    }
    
    protected void OnClickPrintButton()
    {
        var report = LoadSimpleList();
        
        StiReportResponse.PrintAsPdf(report);
        //StiReportResponse.PrintAsHtml(report);
    }
    
    protected void OnClickExportButton()
    {
        var report = LoadSimpleList();
        
        StiReportResponse.ResponseAsPdf(report);
        //StiReportResponse.ResponseAsExcel2007(report);
        //StiReportResponse.ResponseAsPng(report);
        //StiNetCoreReportResponse.ResponseAsJson(report);
    }
}
```


If the **Razor** page does not have components for working with reports (viewer or designer), it is necessary to pre-initialize the reporting tool. You can do this by overriding the standard **OnInitializedAsync** event of a report by adding a special static method, **StiBlazorHelper.Initialize()**, to which you need to pass a **JSRuntime** object as input. After that, the actions for exporting and printing the report will work correctly.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@inject IJSRuntime JSRuntime;

protected override Task OnInitializedAsync()
{
    StiBlazorHelper.Initialize(JSRuntime);
    
    return base.OnInitializedAsync();
}
```
