# Calling Designer from Viewer

The **Angular Viewer** component has the ability to call the report designer. The special **Design** button in the toolbar of the viewer (the button is disabled by default) should be used. To use this feature, you should set the **ShowDesignButton** property to **true**, and also to define the **DesignReport** event handler.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Actions.DesignReport = "DesignReport";
    options.Toolbar.ShowDesignButton = true;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}

public IActionResult DesignReport()
{
    StiReport report = StiAngularViewer.GetReportObject(this);
    ViewBag.ReportName = report.ReportName;
    
    return View("Designer");
}
...
```


> **Information**
>
> The viewer does not run the designer, it only calls the specified action, in which you can get all the necessary parameters. Then, in the action, you can implement redirection to another View, which contains the report designer.
