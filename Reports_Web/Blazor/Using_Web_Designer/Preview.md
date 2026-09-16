# Preview

The **Blazor Designer** component has the mode of an editable report preview. To view a report, you should go to an appropriate bookmark in the designer window. The template will be rendered and displayed in the rendered viewer.


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Designer.Preview_1.png)

There is the ability to perform some necessary actions before previewing a report, for example: connect data for a report. To do it, you should define the **OnPreviewReport** event, which will be invoked before viewing a report.


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
        report.Load("Reports/Simple List.mrt");
        
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
