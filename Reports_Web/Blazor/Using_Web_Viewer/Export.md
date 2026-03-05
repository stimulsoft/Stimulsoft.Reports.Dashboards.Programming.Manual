# Exporting Reports

The **Blazor Viewer** component allows you to export a displayed report to various formats such as **PDF**, **HTML**, **Word**, **Excel**, text, etc. The export function doesn`t require additional settings in the viewer.


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Viewer.Export_1.png)

If you need to make any actions before exporting a report, you can set the special **OneExportReport** event.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer OnExportReport="@OnExportReport" />

@code
{
    private void OnExportReport(StiExportReportEventArgs args)
    {
        // Some code before export
        // ...
    }
}
```

### Export Settings

Each report export format of the Blazor Viewer has a lot of settings, and each setting has its values by default. Sometimes you need other values by default. The special **DefaultSettings** property of the Viewer is used for this. You can find it in the export options. This property is the container of all export settings used by default.


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
        
        //PDF default settings
        Options.Exports.DefaultSettings.ExportToPdf.ImageQuality = 0.75f;
        Options.Exports.DefaultSettings.ExportToPdf.ImageFormat = Stimulsoft.Report.Export.StiImageFormat.Color;
        
        //HTML default settings
        Options.Exports.DefaultSettings.ExportToHtml.UseEmbeddedImages = true;
        Options.Exports.DefaultSettings.ExportToHtml.ExportMode = Stimulsoft.Report.Export.StiHtmlExportMode.Div;
    }
}
```

If required, you can completely hide the display of the export dialog windows. The exporting will always be done with the settings by default. To do this, you just need to set the false value for the **ShowExportDialog** property.


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
        Options.Exports.ShowExportDialog = false;
    }
}
```

The **Blazor Viewer** component contains about 20 various export formats, and sometimes you need to disable some of them. It allows you to load the interface and simplify the use of the Viewer. To disable not used export formats, just set the **false** value for corresponding viewer properties, given in the list below.


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
        Options.Exports.ShowExportDialog = true;
        Options.Exports.ShowExportToDocument = true;
        Options.Exports.ShowExportToPdf = true;
        Options.Exports.ShowExportToXps = true;
        Options.Exports.ShowExportToPowerPoint = true;
        Options.Exports.ShowExportToHtml = true;
        Options.Exports.ShowExportToHtml5 = true;
        Options.Exports.ShowExportToMht = true;
        Options.Exports.ShowExportToText = true;
        Options.Exports.ShowExportToRtf = true;
        Options.Exports.ShowExportToWord2007 = true;
        Options.Exports.ShowExportToOpenDocumentWriter = true;
        Options.Exports.ShowExportToExcel = true;
        Options.Exports.ShowExportToExcelXml = true;
        Options.Exports.ShowExportToExcel2007 = true;
        Options.Exports.ShowExportToOpenDocumentCalc = true;
        Options.Exports.ShowExportToCsv = true;
        Options.Exports.ShowExportToDbf = true;
        Options.Exports.ShowExportToXml = true;
        Options.Exports.ShowExportToDif = true;
        Options.Exports.ShowExportToSylk = true;
    }
}
```

The **Blazor Viewer** component has a feature, which allows you to disable the report export menu. To do this, you should set the **ShowSaveButton** property to **false**.


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
        Options.Toolbar.ShowSaveButton = false;
    }
}
```
