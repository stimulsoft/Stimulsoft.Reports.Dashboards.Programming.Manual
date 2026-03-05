# Showing Reports and Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.


> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `Report.Render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer. Likewise, when using the compilation mode, you need to call the `Report.Compile()` method only if you have actions to perform with the compiled report before it is built and shown in the viewer.

To show the report, you need to add the **StiMvcViewer** component to the page, set it to the minimum required properties, and specify the necessary actions in the view controller.

**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
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
    //report.Load(Server.MapPath("~/Content/Dashboard.mrt"));
    
    return StiMvcViewer.GetReportResult(report);
}

public ActionResult ViewerEvent()
{
    return StiMvcViewer.ViewerEventResult();
}
...
```

In the above example, the processing of two actions of the viewer is added. The **GetReport** action returns the report prepared for preview. The **ViewerEvent** action handles the viewer events.


> **Information**
>
> The **ViewerEvent** action is mandatory. Without it, the correct operation of the viewer is not possible.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Viewer.Showing_Reports_1.png)

If the report is not rendered before showing, the **HTML5 Viewer** component will automatically render it. Thus, you can use report templates, rendered reports, and reports in the form of classes to show the report.


**HomeController.cs**

```csharp
...
public ActionResult GetReport()
{
    StiReport report = new StiReport();
    report.LoadDocument(Server.MapPath("~/Content/SimpleList.mdc"));
    
    return StiMvcViewer.GetReportResult(report);
}
...
```


**HomeController.cs**

```csharp
...
public ActionResult GetReport()
{
    StiReport report = new StiReportCompiledClass();
    
    return StiMvcViewer.GetReportResult(report);
}
...
```

Since the dashboard is not a static document and requires data to work, the format of the rendered MDC document is not available for it. Instead, it is possible to use a snapshot of the report in the MRT format, which contains all the data necessary for the dashboard to work and can be correctly displayed in the viewer.


**Default.aspx.cs**

```csharp
...
public ActionResult GetReport()
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("~/Reports/Snapshot.mrt"));
    
    return StiMvcViewer.GetReportResult(report);
}
...
```

### Loading custom fonts

You can load custom fonts using the **StiFontCollection** class, having specified the file that contains a font. To do this, you should call the static method in the controller constructor to load a font.


**ViewerController.cs**

```csharp
...
public class ViewerController : Controller
{
    static ViewerController()
    {
        Stimulsoft.Base.StiFontCollection.AddFontFile(Server.MapPath("~/fonts/my-font/font-name.ttf"));
    }
}
...
```
