# Creating New Reports and New Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To run the report designer with a new (empty) report, it is enough to create a new report in the **GetReport** action and return it to the designer. If necessary, you can load data for the report, or perform any other necessary actions.


**Index.cshtml**

```
...
@Html.StiNetCoreDesigner(new StiNetCoreDesignerOptions() {
    Actions =
    {
        GetReport = "GetReport"
    }
})
...
```


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostGetReport()
{
    StiReport report = new StiReport();
    
    return StiNetCoreDesigner.GetReportResult(this, report);
}
...
```

You can also create a new report using the main menu of the designer. The **CreateReport** action is used to load data for a new report or perform any other necessary actions. This action will be called when creating a new empty report or when creating a report using the wizard.


**Index.cshtml**

```
...
@Html.StiNetCoreDesigner(new StiNetCoreDesignerOptions() {
    Actions =
    {
        CreateReport = "CreateReport"
    }
})
...
```


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostCreateReport()
{
    StiReport report = new StiReport();
    //var newDashboard = StiReport.CreateNewDashboard();
        
    // Register data for the new report, if necessary
    DataSet data = new DataSet("Demo");
    data.ReadXml(StiNetCoreHelper.MapPath(this, "Data/Demo.xml"));
    report.RegData(data);
    //newDashboard.RegData(data);
    report.Dictionary.Synchronize();
    //newDashboard.Dictionary.Synchronize();
    
    return StiNetCoreDesigner.GetReportResult(this, report);
    //return StiNetCoreDesigner.GetReportResult(this, newDashboard);
}
...
```
