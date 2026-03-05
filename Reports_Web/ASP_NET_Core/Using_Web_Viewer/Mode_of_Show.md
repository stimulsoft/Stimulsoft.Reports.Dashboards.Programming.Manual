# Viewing Modes

The **HTML5 Viewer** component has two modes for displaying reports - with and without scrollbars. By default, the view mode without scrollbars is set. To enable the scrollbar view mode, set the value of the **ScrollbarsMode** property to **true**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Appearance =
    {
        ScrollbarsMode = true
    }
})
...
```

In the first mode (without scrollbars), the viewer displays a page or report as a whole, automatically stretching the preview space. If the width and height are specified, the viewer will truncate the page that is out of bounds. In the second mode, unlike the first one, when the page is out of bounds of the viewer's size, no truncation will be performed. Scrollbars will appear, using which you can view the entire page or report.


> **Information**
>
> In the report mode with scrollbars, you should set the height of the viewer, otherwise the default height will be set to **650 pixels**.

The **HTML5 Viewer** component provides the full-screen report and dashboard mode. By default, the standard view mode is enabled, the viewer has the specified dimensions in the settings. To enable the full-screen mode, set the **FullScreenMode** property to **true**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Appearance =
    {
        FullScreenMode = true
    }
})
...
```

Also, to enable or disable the full-screen mode, you can use the corresponding button on the control panel of the viewer.


The **HTML5 Viewer** component has three modes to display reports - page-by-page, entire report, and tabular display of report pages. To control the modes, the **ViewMode** property is used. It can have one of the specified values - **SinglePage**, **Continuous**, **MultiplePages**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Toolbar =
    {
        ViewMode = StiWebViewMode.SinglePage
    }
})
...
```

The **HTML5 Viewer** component supports interaction on a regular PC display and works with a touchscreen of screens and mobile devices. The **InterfaceType** property allows controlling the interface modes. The property can have one of the following values:

* **Auto** – the viewer's interface is determined automatically depending on the device the report is displayed on. That is the default value.

* **Mouse** – the standard interface with a mouse control will be used for all the screen types.

* **Touch** – the Touch interface will be used to control the viewer. The interface design was optimized for the 'touchscreen' display types. The viewer interface elements have been increased in size to simplify the control of the viewer and to improve its usability.

* **Mobile** - the Mobile interface will be used to control the viewer for all the screen types. The Mobile interface was designed to control the viewer using the mobile smartphone display. This interface design was simplified and adapted to use with smartphones.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Appearance =
    {
        InterfaceType = StiInterfaceType.Auto
    }
})
...
```

![](../../../images/topics/Reports_Web.ASP_NET_Core.Using_Web_Viewer.Mode_of_Show_1.png)
