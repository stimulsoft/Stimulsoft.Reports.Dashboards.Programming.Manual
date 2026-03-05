# Creating New Reports

To run the report designer with a new (empty) report, it is enough to create a new report in the **GetReport** action and return it to the designer. If necessary, you can load data for the report, or perform any other necessary actions.


**Index.cshtml**

```
...
@Html.StiNetCoreDesignerFx(new StiNetCoreDesignerFxOptions() {
    Actions =
    {
        GetReport = "GetReport"
    }
})
...
```


**HomeController.cs**

```csharp
...
public IActionResult GetReport()
{
    StiReport report = new StiReport();
    
    return StiNetCoreDesignerFx.GetReportResult(this, report);
}
...
```

You can also create a new report using the main menu of the designer. The **CreateReport** action is used to load data for a new report or perform any other necessary actions. This action will be called when creating a new empty report or when creating a report using the wizard.


**Index.cshtml**

```
...
@Html.StiNetCoreDesignerFx(new StiNetCoreDesignerFxOptions() {
    Actions =
    {
        CreateReport = "CreateReport"
    }
})
...
```


**HomeController.cs**

```csharp
...
public IActionResult CreateReport()
{
    StiReport report = new StiReport();
        
    // Register data for the new report, if necessary
    DataSet data = new DataSet("Demo");
    data.ReadXml(StiNetCoreHelper.MapPath(this, "Data/Demo.xml"));
    report.RegData(data);
    report.Dictionary.Synchronize();
    
    return StiNetCoreDesignerFx.GetReportResult(this, report);
}
...
```
