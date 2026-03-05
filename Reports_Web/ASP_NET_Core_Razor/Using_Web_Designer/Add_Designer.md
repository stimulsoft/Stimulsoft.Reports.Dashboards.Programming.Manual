# Editing Reports and Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To edit a report template, you should add the **StiNetCoreDesigner** component to a page, set the minimum required settings for it, and define necessary actions in the page event handler.


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


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostGetReport()
{
    // Create the report object
    StiReport report = new StiReport();

    // Load report or dashboard
    report.Load(StiNetCoreHelper.MapPath(this, "Reports/SimpleList.mrt"));
    //report.Load(StiNetCoreHelper.MapPath(this, "Reports/Dashboard.mrt"));

    return StiNetCoreDesigner.GetReportResult(this, report);
}

public IActionResult OnGetDesignerEvent()
{
    return StiNetCoreDesigner.DesignerEventResult(this);
}

public IActionResult OnPostDesignerEvent()
{
    return StiNetCoreDesigner.DesignerEventResult(this);
}
...
```


![](../../../images/topics/Reports_Web.ASP_NET_Core_Razor.Using_Web_Designer.Add_Designer_1.png)

The **GetReport** action is used to load an editable report template. It is called automatically after the report designer is loaded. The **DesignerEvent** action is designed to process various additional designer actions, such as working with data and components, previewing reports and others.


> **Information**
>
> The **DesignerEvent** action is mandatory. Without it, the correct work of the designer is impossible. The action is called for two types of requests: **OnGet** – a component requests necessary resources for work, such as CSS styles, JS scripts, and images; **OnPost** – all other actions of the designer.
