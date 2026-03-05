# Calling Designer from Viewer

The **Blazor** **Viewer** component has the ability to call the report designer. To use this feature, you should define the **OnDesignReport** event handler.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web
@inject NavigationManager NavigationManager

<StiBlazorViewer Report="@Report" OnDesignReport="@OnDesignReport" />

@code
{
    //Report object to use in viewer
    private StiReport Report;
 
    protected override void OnInitialized()
    {
        base.OnInitialized();
         
        var report = new StiReport();
        report.Load("Reports/TwoSimpleLists.mrt");
        Report = report;
    }

    protected void OnDesignReport(StiReportDataEventArgs args)
    {
        //Redirect to the Designer page
        NavigationManager.NavigateTo("Designer?report=" + args.Report.ReportName);
    }
}
```


> **Information**
>
> The viewer doesn’t run the designer. It just calls the specified event in which you can get all necessary parameters. Later in the activity, you can redirect to another page that contains the report designer.
