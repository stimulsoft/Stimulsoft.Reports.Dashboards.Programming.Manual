# Exporting Reports

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **HTML5 Viewer** component allows you to export the displayed report to around three dozen of various formats, such as **PDF**, **HTML**, **Word**, **Excel**, **CSV**. The export function does not require additional settings of the viewer. You may export dashboard to PDF, Excel files.

![](../../images/topics/Reports_JS.Web_Viewer.Export_1.png)

### Export events


To perform any actions before exporting a report, a special **onBeginExportReport** event is used. In this event, you can find out the type of report export, get the report, as well as get the report export settings and, if necessary, change them.


**viewer.html**

```html
...
viewer.onBeginExportReport = function (event) {
    switch (event.format) {
        case Stimulsoft.Report.StiExportFormat.Html:
            event.settings.zoom = 2;  // Set zoom to 200%
            break;
    }
}
...
```

Read more about [viewer events](Viewer_Events.md).


### Export Settings

The **HTML5 Viewer** component contains 7 export formats, and sometimes you need to disable unused formats. This allows you to simplify UI and the use of the viewer. To disable unused export formats, it is enough to set the values for the corresponding properties of the viewer listed in the list below to **false**.

**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.exports.showExportToDocument = false;
options.exports.showExportToPdf = false;
options.exports.showExportToHtml = false;
options.exports.showExportToHtml5 = false;
options.exports.showExportToWord2007 = false;
options.exports.showExportToExcel2007 = false;
options.exports.showExportToCsv = false;
...
```

Also, if required, you can completely remove displaying dialog boxes of export, the export will always be carried out with the default settings. You should to set the value of the **showExportDialog** property to **false**.

**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.exports.showExportDialog = false;
...
```

**Export Report from Code**


Also you can export the report using code. You can use the special **exportDocument()** method on the report object.


**viewer.html**

```html
...
// Create a new report instance
var report = new Stimulsoft.Report.StiReport();
// Load report from url
report.loadFile("../reports/SimpleList.mrt");
// Render report
report.renderAsync(function(){
    report.exportDocument(Stimulsoft.Report.StiExportFormat.Pdf); // Export report to PDF format
});
...
```
