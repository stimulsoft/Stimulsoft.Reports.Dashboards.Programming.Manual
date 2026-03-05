# Creating New Reports

It's enough to create a new object in the **OnInitialized** event to run the designer with a new report. If required, you can preload data for your report or perform some other necessary actions.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorDesigner Report="@Report" />

@code
{
    //Report object to use in designer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Create empty report object
        var report = new StiReport();
        
        //Assing report object to designer
        Report = report;
    }
}
```

Also, you can create a new report using the main menu of the designer. You can use the **OnCreateReport** event to preload data for a new report or perform other necessary actions. This event will be processed when creating a new blank report from the main menu or when creating a report using the wizard.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Web

<StiBlazorDesigner Report="@Report" OnCreateReport="@OnCreateReport"/>

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
    
    private void OnCreateReport(StiReportDataEventArgs args)
    {
        //Delete connections in the report template 
        args.Report.Dictionary.Databases.Clear();

        //Load new data from XML file
        var data = new System.Data.DataSet();
        data.ReadXml("Data/Demo1.xml");
        
        args.Report.RegData(data);
        args.Report.Dictionary.Synchronize();
    }
}
```
