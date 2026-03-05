# Printing Reports

Several options of report printing are envisaged in the **Blazor Viewer** component. Each of them has its features, advantages, and disadvantages.


**Print to PDF**

Printing will be performed with the help of report exporting to **PDF format**. Advantages include great accuracy of location and report elements printing in comparison with other printing options. Among the disadvantages, we can mention the obligatory presence of a plug-in installed in the browser for viewing PDF files (modern Web browsers have an embedded tool for viewing and printing PDF files).


**Print with Preview**

Report printing will be performed in the separate pop-up window of a browser in the **Blazor Viewer**. A report can be previewed and then sent to the printer or copied to another place as text or an HTML code. Its advantages contain cross-browser compatibility when printing, the absence of need for special plug-ins installation. However, there is one disadvantage; it is relatively low accuracy of report elements location, tied features of the implementation of HTML formatting.


**Print without Preview**

Report printing will be performed directly in the printer without preview. After selection of this, system print dialog displays. So as printing in this mode is done in HTML, print quality is analogous to report printing quality with the Preview.


> **Information**
>
> When printing to HTML, you should make sure a report page parameters correspond to the printer page parameters (the size of paper, orientation, fields, indents) and check such browser print settings as indents, headers, and footers, the printing of background images, color printing.

You don't need additional settings of the Viewer for print functions to work. If you need to make some actions before a report print, you can specify the special **OnPrintReport** event.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer OnPrintReport="@OnPrintReport" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;
    
    private void OnPrintReport(StiPrintReportEventArgs args)
    {
        // Some code before print
        // ...
    }
}
```

### Report printing setting

The menu with print options is displayed when selecting a report print in the Viewer panel. The **Blazor Viewer** component has a feature to set the requested print mode forcibly. To use this option, you should set the **PrintDestination** property to one of the **StiPrintDestination** enum values specified below.

**Default** – when selecting a printing, the menu (property value by default) will be displayed;

**Pdf** – printing in PDF format;

**Direct** – printing in an HTML format directly to the Printer, the systemic print dialog will be displayed;

**WithPreview** – printing in HTML format with the Preview in a pop-up window.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;

    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        Options = new StiBlazorViewerOptions();
        Options.Toolbar.PrintDestination = StiPrintDestination.Default;
    }
}
```

The HTML5 component has a feature, which allows you to disable report printing. To do this, you should set the **ShowPrintButton** property to **false**.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options"></StiBlazorViewer>

@code
{
    //Options object
    private StiBlazorViewerOptions Options;

    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        Options = new StiBlazorViewerOptions();
        Options.Toolbar.ShowPrintButton = true;
    }
}
```
