# Using Themes

The **HTML5 Viewer** component can change the appearance of visual controls. To change the theme, use the **Theme** property, which can take one of the values of the StiViewerTheme enumeration.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1",
    new StiMvcViewerOptions() {
        Theme = StiTheme.Office2022WhiteTeal
})
...
```

There are currently **8 themes** available with different color accents. As a result, **more than 60** variants of the appearance are available. This allows you to customize the appearance of the viewer for almost any design of the Web project.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Viewer.Using_Themes_1.png)


By default, the viewer has only the top toolbar on which all the report controls are located. If necessary, the toolbar can be split into top and bottom parts. The top panel will contain the menu for printing and exporting the report and the buttons for working with parameters and bookmarks. The bottom panel will contain controls to switch between the report pages and setting the zoom of pages. To enable this mode, enable the **ToolbarDisplayMode** property. It has values **Simple** and **Separated**.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1",
    new StiMvcViewerOptions() {
        Appearance =
        {
            ScrollbarsMode = true
        },
        Toolbar =
        {
            DisplayMode = StiToolbarDisplayMode.Separated
        }
})
...
```


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Viewer.Using_Themes_2.png)

In addition, it is possible to set the appearance parameters for the main elements of the viewer. For example, you can change the font and color of the control panel inscriptions of the viewer, set the background of the viewer, set the color of page borders, etc. Below is a list of available properties that change the appearance of the viewer and their default values.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1",
    new StiMvcViewerOptions() {
        Appearance =
        {
            BackgroundColor = Color.White,
            PageBorderColor = Color.Blue,
            ShowPageShadow = true
        },
        Toolbar =
        {
            BackgroundColor = Color.White,
            BorderColor = Color.Gray,
            FontColor = Color.Black,
            FontFamily = "Arial"
        }
})
...
```
