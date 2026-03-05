# Work with Parameters

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To work with report parameters in the **HTML5 Viewer**, there is a special settings panel. To add a parameter to the panel, you need to define a variable in a report requested by the user. When viewing a report in the viewer, such a variable will be automatically added to the settings panel. It supports all report variables (normal variables, date and time, borders, lists, etc.).


![](../../../images/topics/Reports_Web.ASP_NET_Core.Using_Web_Viewer.Work_with_Parameters_1.png)

To work with reports with parameters, no additional viewer settings are required. If you need to perform some actions before applying the parameters, you can define a special **Interaction** action.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Actions =
    {
        Interaction = "ViewerInteraction"
    }
})
...
```


**HomeController.cs**

```csharp
...
public IActionResult ViewerInteraction()
{
    // Some code before any interaction
    // ...
    
    return StiNetCoreViewer.InteractionResult(this);
}
...
```

This action is called during any interactive actions of the viewer. If you need to perform any actions only when applying report parameters, you can use the parameters of the viewer. The viewer parameters are represented as an object of the **StiRequestParams** class. They are passed to any server-side on any request and contain all necessary information and states of the client part of the viewer. To determine the type of action of the viewer, it is enough to check the **Action** property of the viewer parameters.


**HomeController.cs**

```csharp
...
public IActionResult ViewerInteraction()
{
    StiRequestParams requestParams = StiNetCoreViewer.GetRequestParams(this);
    if (requestParams.Action == StiAction.Variables)
    {
        // Some code before apply parameters
    }
    
    return StiNetCoreViewer.InteractionResult(this);
}
...
```

If you do not need to work with parameters, you can completely disable this feature. To do this, use the **ShowParametersButton** property in the **Toolbar** section of properties, which should be set to **false**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Toolbar =
    {
        ShowParametersButton = false
    }
})
...
```


> **Information**
>
> The options panel will not be displayed with such a viewer configuration, even if the parameters are present in the displayed report.
