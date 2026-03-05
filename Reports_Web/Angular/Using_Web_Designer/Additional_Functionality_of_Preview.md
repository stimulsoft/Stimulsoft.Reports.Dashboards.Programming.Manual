# Additional Features of Preview

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The preview window of the **HTML5 Designer** component has a fully functional interactive **Angular Viewer** that can print and export reports, supports working with report parameters, dynamic sorting, interactive reports, collapsing and etc. To use these features, you do not need any additional settings for the report designer.


In any of the above actions, you can work with the report template, for example, change its properties and parameters, connect new data for rendering.


**Index.cshtml**

```
...
@Html.StiNetCoreDesigner(new StiNetCoreDesignerOptions() {
    Actions =
    {
        ExportReport = "ExportReport"
    }
})
...
```


**HomeController.cs**

```csharp
...
public IActionResult ExportReport()
{
    StiReport report = StiNetCoreDesigner.GetActionReportObject(this);
    // ...
    
    return StiNetCoreDesigner.ExportReportResult(this, report);
}
...
```


> **Information**
>
> If you do not need any of these additional options to preview the report (for example, exporting or printing a report), you can disable them using the appropriate properties of the **HTML5 Designer** component.
