# Showing Reports

> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `report.render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer.

To show the report, you need to add the **stimulsoft-viewer-angular** component to the template and set it to the minimum required properties: request URL template & action name.


**component.ts**

```typescript
...
<stimulsoft-viewer-angular [requestUrl]="'http://server.url:51528/Viewer/{action}'" [action]="'Post'" ></stimulsoft-viewer-angular>
...
```

And in the view controller, specify the necessary actions.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);            
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}

public IActionResult ViewerEvent()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
        
    if (requestParams.Action == StiAction.GetReport)
    {
        return GetReport(reportName);
    }
    return StiAngularViewer.ProcessRequestResult(this);
}

public IActionResult GetReport()
{
    StiReport report = new StiReport();
    report.Load(StiAngularHelper.MapPath(this, "Reports/SimpleList.mrt"));
     
    return StiAngularViewer.GetReportResult(this, report);
}
...
```

In the above example, processing of actions of the viewer is added. Angular viewer initialized by action configured in [requestUrl] & [action] here you need to specify **StiAngularViewerOptions** and **ViewerEvent** action. The **ViewerEvent** action handles the viewer events and if action is **GetReport** returns the report prepared for preview.


> **Information**
>
> The **ViewerEvent** action is mandatory. Without it, the correct operation of the viewer is not possible.


![](../../../images/topics/Reports_Web.Angular.Using_Web_Viewer.Showing_Reports_1.png)

If the report was not rendered before showing, the **Angular Viewer** component will automatically render it. So you can use report templates and rendered reports to display reports.


**HomeController.cs**

```csharp
...
public IActionResult GetReport()
{
    StiReport report = new StiReport();
    report.LoadDocument(StiAngularHelper.MapPath(this, "Reports/SimpleList.mdc"));
    
    return StiAngularViewer.GetReportResult(this, report);
}
...
```
