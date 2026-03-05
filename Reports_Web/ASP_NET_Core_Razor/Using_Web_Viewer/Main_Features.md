# Basic Features

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The main features of the viewer include the following operations:

- Displaying the report.
- Switching between the report pages.
- Changing the scale.
- Displaying the preview mode.

All specified operations are performed in the AJAX mode without restarting the browser page. For the correct work of these operations, you should define a special ViewerEvent action.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Actions =
    {
        ViewerEvent = "ViewerEvent"
    }
})
...
```


**Index.cshtml.cs**

```csharp
...
public IActionResult OnGetViewerEvent()
{
    // Some code before loading the viewer resources
    // ...

    return StiNetCoreViewer.ViewerEventResult(this);
}

public IActionResult OnPostViewerEvent()
{
    // Some code before the viewer actions
    // ...

    return StiNetCoreViewer.ViewerEventResult(this);
}
...
```


> **Information**
>
> The **ViewerEvent** action is mandatory. Without it, the viewer can’t work correctly. The action is called for two types of requests: **OnGet** – the component requests the resources necessary for work, such as CSS styles, JS scripts and images; **OnPost** – all other actions of the viewer.

The **ViewerEvent** action returns a prepared HTML page of the report (or set of pages), built taking into account the current state of the viewer. If necessary, you can change the parameters of the current report in the specified action and update the report data in case of interactive actions of the viewer.
