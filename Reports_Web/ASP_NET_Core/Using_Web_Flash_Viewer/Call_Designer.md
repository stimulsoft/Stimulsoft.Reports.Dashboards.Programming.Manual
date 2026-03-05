# Calling Designer from Viewer

The **Flash Viewer** component has the ability to call the report designer. The special **Design** button in the toolbar of the viewer (the button is disabled by default) should be used. To use this feature, you should set the **ShowDesignButton** property to **true**, and also to define the **DesignReport** event handler.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
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
public IActionResult DesignReport()
{
    return View("Designer");
}
...
```


> **Information**
>
> The viewer does not run the designer itself, it only calls the specified event and passes the previewed report as arguments. In the event, you can set redirection to another View, on which the report designer is placed.
