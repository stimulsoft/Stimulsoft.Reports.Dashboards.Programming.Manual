# Vieweing Modes

There are two modes of report display - with scroll bars and without them. The mode to view reports without scroll bars is set by default. To disable the viewing mode with scroll bars, you should set the **ScrollbarsMode** property to **true**.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Init options object
        Options = new StiBlazorViewerOptions();
        Options.Appearance.ScrollbarsMode = false;
    }
}
```

The Viewer displays a page or a report entirely, automatically stretching the viewer in the first mode (without scroll bars). If the sizes in width and heights are specified, the Viewer will crop the page that has gone beyond the margins. In the second mode, unlike the first one, the cropping won`t be made when a page goes beyond the Viewer size. Instead, scroll bars appear, with the help of them, you can view the entire page or a report.


> **Information**
>
> You should set the height of the Viewer in the report viewing mode; otherwise, the height is **650 pixels** will be set by default.

The mode of a report or a dashboard full-screen display is envisaged in the **Blazor Viewer** component. The standard viewing mode is enabled by default. The Viewer has specified sizes in settings. To enable the full-screen mode of viewing, just set the **true** value for the **FullScreenMode** property.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Init options object
        Options = new StiBlazorViewerOptions();
        Options.Appearance.FullScreenMode = true;
    }
}
```

Also, to enable or disable the full-screen mode, you can use the corresponding button in the Viewer toolbar.


There are three report display modes in the **Blazor Viewer** - page display, full report as a ribbon, and tabular display of report pages. The **View Mode** property is used for this. This property accordingly takes one of the following values - **SinglePage**, **Continuous**, **MultiplePages**.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Init options object
        Options = new StiBlazorViewerOptions();
        Options.Toolbar.ViewMode = StiWebViewMode.SinglePage;
    }
}
```

The support of work with a simple computer as well as with touchscreens and mobile devices is realized in the **Blazor Viewer** component. The Interface type property is intended for managing modes. This property takes one of the following values:

* **Auto** - the Viewer interface type will be selected automatically depending on the device used (value by default).

* **Mouse** **-** forced using the standard interface for managing the viewer.

* **Touch** **-** forced using the Touch interface for managing the viewer with the help of the touchscreen monitor. In this mode, the viewer interface elements have increased sizes for comfortable managing.

* **Mobile** - forced use of Mobile interface for managing viewer with the help smartphone screen, in this mode the viewer interface has a simplified view and adapted for managing with the help of a mobile device.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Init options object
        Options = new StiBlazorViewerOptions();
        Options.Appearance.InterfaceType = StiInterfaceType.Auto;
    }
}
```


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Viewer.Mode_of_Show_1.png)
