# Editing Reports

To edit a report template, you need to add a **StiMvcDesignerFx** component to the page, specify the minimum necessary settings for it, and set the necessary actions in the view controller.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesignerFx("MvcDesignerFx1", 
    new StiMvcDesignerFxOptions() {
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
public ActionResult GetReport()
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("~/Content/SimpleList.mrt"));
    
    return StiMvcDesignerFx.GetReportResult(report);
}

public ActionResult DesignerEvent()
{
    return StiMvcDesignerFx.DesignerEventResult();
}
...
```


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Flash_Designer.Editting_Report_1.png)

The **GetReport** action is used to load an editable report template. It is called automatically after the report designer is loaded. The **DesignerEvent** action is designed to process various additional designer actions, such as working with data, previewing the report, viewing the C#/VB.Net report code, and others.


> **Information**
>
> The **DesignerEvent** action is mandatory. Without it, the correct work of the designer is impossible.
