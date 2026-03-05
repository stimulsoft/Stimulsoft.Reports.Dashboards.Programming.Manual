# Basic Features

The main features of the viewer include the following operations: displaying the report, switching between the report pages, changing the scale and displaying the preview mode. All specified operations are performed in the AJAX mode without restarting the browser page. For the correct work of these operations, you should define a special **ViewerEvent** action.


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
    // Some code before viewer event
    // ...
    
    return StiAngularViewer.ViewerEventResult(this);
}
...
```


> **Information**
>
> This action is mandatory. Without it, the correct operation of the viewer is not possible.

The **ViewerEvent** action returns a prepared HTML page of the report (or set of pages), built taking into account the current state of the viewer. If necessary, you can change the parameters of the current report in the specified action, as well as update the report data in case of interactive actions of the viewer.
