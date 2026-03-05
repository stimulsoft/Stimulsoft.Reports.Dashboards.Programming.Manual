# Additional Features of Preview

The window of report viewing of the **Blazor Designer** is a full-fledged interactive viewer, which can print and export a report. Besides, it supports the work with their parameters. Also, interactive actions are supported among them - dynamic sorting, drill-down, collapsing. To use these options, you don't need any additional settings of the report designer.


You can make manipulations with a report template in any of the above actions. For example, you can change properties and parameters, connect new data for rendering. When exporting a report, you can get the export format, read or change its settings.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorDesigner Report="@Report" OnExportReport="@OnExportReport"/>

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
        report.Load("Reports/Simple List.mrt");
        
        //Assing report object to designer
        Report = report;
    }
    
    private void OnExportReport(StiExportReportEventArgs args)
    {
        //Current export format
        var exportFormat = args.Format;
        
        //Current export settings
        var exportSettings = args.Settings;
    
        //Load new data from XML file
        var data = new System.Data.DataSet();
        data.ReadXml("Data/Demo1.xml");
        
        args.Report.RegData(data);
    }
}
```


> **Information**
>
> Suppose some of the specified additional options of the Report Preview are not required (for example, exporting or report printing). In that case, you can disable them using the appropriate options of the **Blazor Designer**.
