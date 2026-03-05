# Basic Features

The main features of the viewer include the following operations:

- Displaying the report.
- Switching between the report pages.
- Changing the scale.
- Displaying the preview mode.

All specified operations are performed in the AJAX mode without restarting the browser page. For the correct work of these operations, you should define a special ViewerEvent action.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Actions =
        {
            ViewerEvent = "ViewerEvent"
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult ViewerEvent()
{
    // Some code before viewer event
    // ...

    return StiMvcViewer.ViewerEventResult();
}
...
```


> **Information**
>
> This action is mandatory. Without it, the correct operation of the viewer is not possible.

The **ViewerEvent** action returns a prepared HTML page of the report (or set of pages), built taking into account the current state of the viewer. If necessary, you can change the parameters of the current report in the specified action and update the report data in case of interactive actions of the viewer.
