# Printing Reports

> **Information**
>
> Please note that the print option is available only for reports, and not for dashboards.

The **HTML5 Viewer** component provides several options for printing a report. Each has its advantages and disadvantages.


**Print to PDF**

Printing will be done by exporting the report to PDF. The advantages are greater accuracy of positioning and printing of the report elements compared to other printing options. Among the drawbacks, one can mention the mandatory presence of a plug-in installed in a web browser for viewing PDF files (modern browsers have embedded PDF viewer and printer).


**Print with Preview**

The report will be printed in a separate pop-up browser window in HTML. The report can be previewed and then sent to the printer or copied to another location as text or HTML code. Advantages - cross-browser compatibility when printing, no need to install special plug-ins. The disadvantage is the relatively low accuracy of the position of the report elements due to the peculiarities of the implementation of HTML formatting.


**Print without Preview**

The report will be printed directly to the printer without preview. After selecting this menu item, the system print dialog is displayed. Since printing in this mode is carried out in the HTML format, the print quality is similar to printing a report with a preview.


> **Information**
>
> When printing to the **HTML format**, you should check the compliance of report page settings and printer parameters (paper size, orientation, margins, indents), as well as check your browser print settings, such as margins, headers, footers, watermarks printing, color printing.

The print function does not require additional settings for the viewer. If you need to perform any actions before printing a report, you can define a special **PrintReport** action.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Actions =
    {
        PrintReport = "PrintReport"
    }
})
...
```


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostPrintReport()
{
    // Some code before print
    // ...
    
    return StiNetCoreViewer.PrintReportResult(this);
}
...
```

### Print setup

If you choose printing a report in the viewer panel, a menu with printing options is displayed. The **HTML5 Viewer** component is able to force the required printing mode. To do this, set the **PrintDestination** property to one of the following values of the **StiPrintDestination** enumeration.

**Default** – the menu will be displayed (the default property value);

**Pdf** – print to the PDF format;

**Direct** – printing to the HTML format directly to the printer, the system print dialog will be displayed;

**WithPreview** – print to the HTML format with preview in a pop-up window.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Toolbar =
    {
        PrintDestination = StiPrintDestination.Default
    }
})
...
```

The **HTML5 Viewer** component is able to completely disable report printing. To do this, set the value of the **ShowPrintButton** property to **false**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Toolbar =
    {
        ShowPrintButton = false
    }
})
...
```
