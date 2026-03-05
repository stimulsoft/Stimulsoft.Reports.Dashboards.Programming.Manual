# Additional Methods

For **Flash Viewer**, there are several additional methods that are used to get the object of the currently viewed report, parameters of the current state of the viewer and other useful data. These methods can be used in any actions of the viewer.


### The GetReportObject() method

Returns the report object with which the viewer is currently working. It is possible to perform the necessary actions with it - register new data sets, change report properties, assign parameters or load another report to the object. Then, the report can be returned to the viewer, specifying it as a parameter in the resulting action method.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiReport report = StiMvcViewerFx.GetReportObject();
    report.ReportName = "MyReportName";
    
    return StiMvcViewerFx.ExportReportResult(report);
}
...
```


### The GetRouteValues() method

Returns values for URLs with which the viewer page was opened. Thus, it is possible to get the initial collection of parameters of the run page of the viewer and use these values for any checks and conditions.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    RouteValueDictionary routeValues = StiMvcViewerFx.GetRouteValues();
    
    return StiMvcViewerFx.ExportReportResult();
}
...
```

You can also get values of URL parameters by parameter name, specifying it as the parameter of the called action of the viewer.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport(string id)
{
    return StiMvcViewerFx.ExportReportResult();
}
...
```


### The GetRequestParams() method

Returns all parameters of the current state of the viewer passed to the server-side. They can be useful for determining the type of action that the viewer is currently executing - for example, to determine the type of export, as well as all action parameters.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiRequestParams requestParams = StiMvcViewerFx.GetRequestParams();
    if (requestParams.ExportFormat == StiExportFormat.Pdf)
    {
        StiReport report = StiMvcViewerFx.GetReportObject();
        
        // Some action with report for the PDF export
        // ...
        
        return StiMvcViewerFx.ExportReportResult(report);
    }

return StiMvcViewerFx.ExportReportResult();
}
...
```


### The GetLocalizationName() method

Returns the name of the requested XML localization file in the **GetLocalization** action. By default, this value is used when generating a response to the viewer. Can be used to manage loading of localization files.


**HomeController.cs**

```csharp
...
public ActionResult GetLocalization()
{
    string name = StiMvcViewerFx.GetLocalizationName();
    string path = "~/Content/Localization/" + name;
    
    return StiMvcViewerFx.GetLocalizationResult(path);
}
...
```


### The GetExportSettings() method

Returns all the parameters of the current report export. The type of the parameter object will correspond to the type of the export selected in the viewer menu. Any export parameters can be changed and passed to the input of the resulting method. In this case, the report will be exported with the parameters transferred.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiExportSettings settings = StiMvcViewerFx.GetExportSettings();
    if (settings.GetExportFormat() == StiExportFormat.Pdf)
    {
        StiPdfExportSettings pdfSettings = (StiPdfExportSettings)settings;
        pdfSettings.EmbeddedFonts = true;
        pdfSettings.AllowEditable = StiPdfAllowEditable.No;
        return StiMvcViewerFx.ExportReportResult(settings);
    }
    
    return StiMvcViewerFx.ExportReportResult();
}
...
```
