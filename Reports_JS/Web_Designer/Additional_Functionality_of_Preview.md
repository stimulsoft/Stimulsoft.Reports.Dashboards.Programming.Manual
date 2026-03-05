# Additional Features of Preview

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The preview window of the **HTML5 Designer** component has a fully functional interactive **HTML5 Viewer** that can print and export reports, supports working with report parameters, dynamic sorting, interactive reports, collapsing and etc. You do not need any additional settings for the report designer to use these features.

**designer.html**

```html
...
designer.viewer.onBeginExportReport = function (event) {
    switch (event.format) {
        case Stimulsoft.Report.StiExportFormat.Html:
            event.settings.zoom = 2;  // Set zoom to 200%
            break;
    }
    console.log("exporting");
}
...
```


> **Information**
>
> If you do not need any of these additional options to preview the report (for example, exporting or printing a report), you can disable them using the appropriate properties of the **HTML5 Designer** component.
