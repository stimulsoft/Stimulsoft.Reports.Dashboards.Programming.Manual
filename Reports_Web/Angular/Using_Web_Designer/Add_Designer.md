# Editing Reports

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To edit a report template, you need to add the **StiNetCoreDesigner**  component to the page, specify the minimum necessary settings for it, and define the necessary actions in the view controller.


**Index.cshtml**

```
...
@Html.StiNetCoreDesigner(new StiNetCoreDesignerOptions() {
    Actions =
    {
        GetReport = "GetReport",
        DesignerEvent = "DesignerEvent"
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
    report.Load(StiNetCoreHelper.MapPath(this, "Reports/SimpleList.mrt"));
    //report.Load(StiNetCoreHelper.MapPath(this, "Reports/Dashboard.mrt"));
    
    return StiNetCoreDesigner.GetReportResult(this, report);
}

public IActionResult DesignerEvent()
{
    return StiNetCoreDesigner.DesignerEventResult(this);
}
...
```


![](../../../images/topics/Reports_Web.Angular.Using_Web_Designer.Add_Designer_1.png)

The **GetReport** action is used to load an editable report template. It is called automatically after the report designer is loaded. The **DesignerEvent** action is designed to process various additional designer actions, such as working with data and components, previewing reports and others.


> **Information**
>
> The **DesignerEvent** action is mandatory. Without it, the correct work of the designer is impossible.
