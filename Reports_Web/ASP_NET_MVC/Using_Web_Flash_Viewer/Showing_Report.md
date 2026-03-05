# Showing Report

To show the report, you need to add the **StiMvcViewerFx** component to the page and set it to the minimum required properties, and, in the view controller, specify the necessary actions.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewerFx("MvcViewerFx1", 
    new StiMvcViewerFxOptions() {
        Actions =
        {
            GetReport = "GetReport",
            ViewerEvent = "ViewerEvent"
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
    
    return StiMvcViewerFx.GetReportResult(report);
}

public ActionResult ViewerEvent()
{
    return StiMvcViewerFx.ViewerEventResult();
}
...
```

In the above example, processing of two actions of the viewer is added. The **GetReport** action returns the report prepared for preview, the **ViewerEvent** action handles the viewer events.


> **Information**
>
> The **ViewerEvent** action is mandatory. Without it, the correct operation of the viewer is not possible.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Flash_Viewer.Showing_Report_1.png)

If the report was not rendered before showing, the **Flash Viewer** component will automatically render it. Thus, you can use report templates, rendered reports, and reports in the form of classes to show the report.


**HomeController.cs**

```csharp
...
public ActionResult GetReport()
{
    StiReport report = new StiReport();
    report.LoadDocument(Server.MapPath("~/Content/SimpleList.mdc"));
    
    return StiMvcViewerFx.GetReportResult(report);
}
...
```


**HomeController.cs**

```csharp
...
public ActionResult GetReport()
{
    StiReport report = new StiReportCompiledClass();
    
    return StiMvcViewerFx.GetReportResult(report);
}
...
```
