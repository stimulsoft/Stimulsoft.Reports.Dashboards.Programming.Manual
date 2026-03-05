# Showing Reports

> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `Report.Render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer. Likewise, when using the compilation mode, you need to call the `Report.Compile()` method only if you have actions to perform with the compiled report before it is built and shown in the viewer.

To display a report, you should add the **StiBlazorViewer** component on the Razor page, add the **StiReport** object, and assign it to the viewer using the Report property. After a report is loaded from a file, it will be displayed in the viewer automatically.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    //Report object to use in viewer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Create empty report object
        var report = new StiReport();
        
        //Load report template
        report.Load("Reports/TwoSimpleLists.mrt");

        //Assing report object to viewer
        Report = report;
    }
}
```

If a report is not rendered before display, the **BlazorViewer** component will render it automatically. This way, to display a report, you can use various types of reports - report templates and already generated reports.


### Loading fonts

The Blazor does not have access to the fonts installed on a computer, so to render a report correctly, you should specify the fonts you used in your report. You can do it with the help of the statistic **StiFontCollection** class by either specifying a file or the Base64 string, which has a necessary font.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    //Report object to use in viewer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Init base font as a file
        Stimulsoft.Base.StiFontCollection.AddFontFile("Fonts/Microsoft Sans Serif.ttf", "Segoe UI");
        
        //Init base font as a Base64 string
        var fontBase64 = "AAEAAAAVAQAABABQRFNJR/W/YxAAA814A...";
        Stimulsoft.Base.StiFontCollection.AddFontBase64(fontBase64, "Segoe UI");
        
        //Create empty report object
        report = new StiReport();
        
        //Load report template
        report.Load("Reports/TwoSimpleLists.mrt");
        
        //Assing report object to viewer
        Report = report;
    }
}
```
