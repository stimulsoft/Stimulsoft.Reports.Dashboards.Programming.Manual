# Calling Designer from Viewer

The **HTML5 Viewer** component has the ability to call the report designer. The special **Design** button in the toolbar of the viewer (the button is disabled by default) should be used. To use this feature, you should set the **ShowDesignButton** property to true and define the **DesignReport** event handler.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Actions =
        {
            DesignReport = "DesignReport"
        },
        Toolbar =
        {
            ShowDesignButton = true
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult DesignReport()
{
    StiReport report = StiMvcViewer.GetReportObject();
    ViewBag.ReportName = report.ReportName;
    
    return View("Designer");
}
...
```


> **Information**
>
> The viewer does not run the designer. It only calls the specified action, in which you can get all the necessary parameters. Then, in action, you can implement a redirection to another View, which contains the report designer.
