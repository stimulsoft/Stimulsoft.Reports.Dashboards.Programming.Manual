# Showing Reports and Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.


> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `Report.Render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer. Likewise, when using the compilation mode, you need to call the `Report.Compile()` method only if you have actions to perform with the compiled report before it is built and shown in the viewer.

To display a report, you should add the **StiNetCoreViewer** component to a page, set the minimum required properties, and define necessary actions in the page event handler.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Actions =
    {
        GetReport = "GetReport",
        ViewerEvent = "ViewerEvent"
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
    
    return StiNetCoreViewer.GetReportResult(this, report);
}

public IActionResult OnGetViewerEvent()
{
    return StiNetCoreViewer.ViewerEventResult(this);
}

public IActionResult OnPostViewerEvent()
{
    return StiNetCoreViewer.ViewerEventResult(this);
}
...
```

In the above example, the processing of two actions of the viewer is added. The **GetReport** action returns the report prepared for preview. The **ViewerEvent** action handles the viewer events.


> **Information**
>
> The **ViewerEvent** action is mandatory. Without it, the viewer can’t work correctly. The action is called for two types of requests: **OnGet** – the component requests the resources necessary for work, such as CSS styles, JS scripts and images; **OnPost** – all other actions of the viewer.


![](../../../images/topics/Reports_Web.ASP_NET_Core_Razor.Using_Web_Viewer.Showing_Reports_1.png)

If the report was not rendered before showing, the **HTML5 Viewer** component will automatically render it. So you can use report templates and rendered reports to display reports.


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostGetReport()
{
    StiReport report = new StiReport();
    report.LoadDocument(StiNetCoreHelper.MapPath(this, "Reports/SimpleList.mdc"));
    
    return StiNetCoreViewer.GetReportResult(this, report);
}
...
```

Since the dashboard is not a static document and requires data to work, the format of the rendered MDC document is not available for it. Instead, it is possible to use a snapshot of the report in the MRT format, which contains all the data necessary for the dashboard to work and be correctly displayed in the viewer.


**Index.cshtml.cs**

```csharp
...
public ActionResult OnPostGetReport()
{
    StiReport report = new StiReport();
    report.Load(StiNetCoreHelper.MapPath("~/Reports/Snapshot.mrt"));
    
    return StiNetCoreViewer.GetReportResult(report);
}
...
```

**Loading custom fonts**

You can connect custom fonts using the **StiFontCollection** class, having specified a file that contains a font. To do this, you should invoke the static method in the page constructor to load the font.


**Index.cshtml.cs**

```csharp
...
public class ViewerController : Controller
{
    static ViewerController()
    {
        Stimulsoft.Base.StiFontCollection.AddFontFile(StiNetCoreHelper.MapPath(this, "/fonts/my-font/font-name.ttf"));
    }
}
...
```
