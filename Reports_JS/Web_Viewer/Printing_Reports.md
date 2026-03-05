# Printing Reports

> **Information**
>
> Please note that the print option is available only for reports, and not for dashboards.

The **HTML5 Viewer** component has several options for printing a report. Each has its own advantages and disadvantages.


### Print to PDF

Printing will be done by exporting the report to the **PDF format**. The advantages are greater accuracy of positioning and printing of the report elements in comparison with other printing options. Among the drawbacks one can mention the mandatory presence of a plug-in installed in a web browser for viewing PDF files (modern browsers have embedded PDF viewer and printer).


> **Information**
>
> Internet Explorer and Edge browsers do not support direct output of PDF content from JavaSctipt code, so when printing as PDF, you will be prompted to save the file, and only then it can be printed.

### Print with Preview

The report will be printed in a separate pop-up browser window in the **HTML format**. The report can be previewed, and then sent to the printer or copied to another location as text or HTML code. The advantages are cross-browser compatibility when printing, no need to install special plug-ins. The disadvantage is the relatively low accuracy of the position of the report elements, due to the issues with implementation of HTML formatting.

### Print without Preview

The report will be printed directly to the printer without preview. After selecting this menu item, the system print dialog is displayed. Since printing in this mode is carried out in the **HTML format**, then the print quality is similar to the quality of printing a report with a preview.

> **Information**
>
> The report is printed using the built-in methods of the current browser, so the presentation of the dialog box may differ in operating systems and browsers. Also, the browser does not allow managing print settings from JavaScript code, so the required settings will need to be performed in the dialog box.

### Print setup

If you choose printing a report in the viewer panel, a menu with printing options is displayed. The **HTML5 Viewer** component is able to force the required printing mode. To do this, set the **printDestination** property to one of the following values of the **StiPrintDestination** enumeration.

**Default** – the menu will be displayed (the default property value);

**Pdf** – print to the PDF format;

**Direct** – printing to the HTML format directly to the printer, the system print dialog will be displayed;

**WithPreview** – print to the HTML format with preview in a pop-up window.


**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.toolbar.printDestination = Stimulsoft.Viewer.StiPrintDestination.Default;
...
```

The **HTML5 Viewer** component is able to completely disable report printing. To do this, set the value of the **showPrintButton** property to **false**.

**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.toolbar.showPrintButton = false;
...
```


### Print Report from Code

Also it is possible to print a report using the code. To do this, you can use the special **print()** method on the report object.

**viewer.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("SimpleList.mrt");
report.renderAsync(function(){
    report.print();
});
...
```


When printing a report, it is possible to specify a print range. The special **StiPagesRange** class is used for this, it is allowed to set the following parameters as the arguments of the constructor.

* Range type (the following values are available **Stimulsoft.Report.StiRangeType.All**, **Stimulsoft.Report.StiRangeType.Pages**, **Stimulsoft.Report.StiRangeType.CurrentPage****);**
* Range as a string representation (page numbers are separated with commas or hyphenated);
* **Current page number.**


**viewer.html**

```html
...
var pageRange = new Stimulsoft.Report.StiPagesRange(Stimulsoft.Report.StiRangeType.CurrentPage, "1,3-8", 5);
report.print(pageRange);
...
```
