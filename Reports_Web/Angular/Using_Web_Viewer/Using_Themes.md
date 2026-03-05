# Using Themes

The **Angular Viewer** component can change the appearance of visual controls. To change the theme, use the **Theme** property, which can take one of the values of the StiViewerTheme enumeration.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Theme = StiViewerTheme.Office2022WhiteTeal;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

There are currently **8 themes** available with different color accents. As a result, **more than 60** variants of the appearance are available. This allows you to customize the appearance of the viewer for almost any design of the Web project.


![](../../../images/topics/Reports_Web.Angular.Using_Web_Viewer.Using_Themes_1.png)

By default, the viewer has only the top toolbar on which all the report controls are located. If necessary, the toolbar can be split into top and bottom parts. The top panel will contain the menu for printing and exporting the report, as well as the buttons for working with parameters and bookmarks. The bottom panel will contain controls to switch between the report pages and setting zoom of pages. To enable this mode, enable the **ToolbarDisplayMode** property. It has values **Simple** and **Separated**.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Appearance.ScrollbarsMode = true;
    options.Toolbar.DisplayMode = StiToolbarDisplayMode.Separated;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```


![](../../../images/topics/Reports_Web.Angular.Using_Web_Viewer.Using_Themes_2.png)

In addition, it is possible to set the appearance parameters for the main elements of the viewer. For example, you can change the font and color of the control panel inscriptions of the viewer, set the background of the viewer, set the color of page borders, etc. Below is a list of available properties that change the appearance of the viewer, and their default values.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Appearance.BackgroundColor = Color.White;
    options.Appearance.PageBorderColor = Color.Blue;
    options.Appearance.ShowPageShadow = true;
    options.Toolbar.BackgroundColor = Color.White;
    options.Toolbar.BorderColor = Color.Gray;
    options.Toolbar.FontColor = Color.Black;
    options.Toolbar.FontFamily = "Arial";
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```
