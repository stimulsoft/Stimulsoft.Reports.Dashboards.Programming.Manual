# Using Themes

The **Blazor Viewer** component has an option to change the design themes of controls. The **Theme** property in the component options is used to change a theme. It may have one of the values of the **StiViewerTheme** enumeration.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Theme="StiViewerTheme.Office2022WhiteCarmine" />
```

There are currently **8 themes** available with different color accents. As a result, **more than 60** variants of the appearance are available. This allows you to customize the appearance of the viewer for almost any design of the Web project.


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Viewer.Using_Themes_1.png)

By default, the Viewer displays only the top toolbar, where there are all controls. If it's necessary, you can divide the toolbar into the top and the lower. The menu of printing and exporting reports will be on the top panel, also the buttons to work with parameters and bookmarks. The lower toolbar will contain elements to switch between report pages and the zoom control menu. The **DisplayMode** property is intended for enabling the specified mode, which can have the **Simple** value mode and the **Separated** mode.


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
        Options.Appearance.ScrollbarsMode = true;
        Options.Toolbar.DisplayMode = StiToolbarDisplayMode.Separated;
    }
}
```


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Viewer.Using_Themes_2.png)

Additionally, you may set the parameters of the main viewer elements. For example, you can change the font and color of the Viewer toolbar titles, set the background of the Viewer, color, etc. Below is the list of available properties, which change the Viewer design and their value by default.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web
@using System.Drawing

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
        Options.Appearance.BackgroundColor = Color.White;
        Options.Appearance.PageBorderColor = Color.Blue;
        Options.Appearance.ShowPageShadow = true;
        Options.Toolbar.BackgroundColor = Color.White;
        Options.Toolbar.BorderColor = Color.Gray;
        Options.Toolbar.FontColor = Color.Black;
        Options.Toolbar.FontFamily = "Arial";
    }
}
```
