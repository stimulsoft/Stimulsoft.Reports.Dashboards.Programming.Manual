# Addtional Methods

For **Flash Designer**, there are several additional methods that are used to get the object of the currently edited report, parameters of the current state of the designer and other useful data. These methods can be used in any actions of the designer.


### The GetReportObject() method

Returns the report object with which the designer is currently working. It is possible to perform the necessary actions with it - register new data sets, change report properties, assign parameters or load another report to the object. Then, the report can be returned to the designer, specifying it as a parameter in the resulting action method.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiReport report = StiMvcDesignerFx.GetReportObject();
    report.ReportName = "MyReportName";
    
    return StiMvcDesignerFx.ExportReportResult(report);
}
...
```


### The GetRouteValues() method

Returns values for URLs with which the designer page was opened. Thus, it is possible to get the initial collection of page parameters to run the designer and use these values for any checks and conditions.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    RouteValueDictionary routeValues = StiMvcDesignerFx.GetRouteValues();
    
    return StiMvcDesignerFx.ExportReportResult();
}
...
```

You can also get values of URL parameters by parameter name, specifying it as the parameter of the called action of the designer.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport(string id)
{
    return StiMvcDesignerFx.ExportReportResult();
}
...
```


### The GetRequestParams() method

Returns all parameters of the current state of the designer passed to the server-side. They can be useful for determining the type of action that the designer is currently executing - for example, to determine the type of export, as well as all action parameters.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiRequestParams requestParams = StiMvcDesignerFx.GetRequestParams();
    if (requestParams.ExportFormat == StiExportFormat.Pdf)
    {
        StiReport report = StiMvcDesignerFx.GetReportObject();
        
        // Some action with report for the PDF export
        // ...
        
        return StiMvcDesignerFx.ExportReportResult(report);
    }

    return StiMvcDesignerFx.ExportReportResult();
}
...
```


### The GetLocalizationName() method

Returns the name of the requested XML localization file in the **GetLocalization** action. By default, this value is used when creating a response to the designer. Can be used to manage loading of localization files.


**HomeController.cs**

```csharp
...
public ActionResult GetLocalization()
{
    string name = StiMvcDesignerFx.GetLocalizationName();
    string path = "~/Content/Localization/" + name;
    
    return StiMvcDesignerFx.GetLocalizationResult(path);
}
...
```


### The GetExportSettings() method

Returns all parameters of the current report export. The type of the parameter object will correspond to the type of export selected in the report preview menu. Any export parameters can be changed and passed to the input of the resulting method. In this case, the report will be exported with the parameters transferred.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiExportSettings settings = StiMvcDesignerFx.GetExportSettings();
    if (settings.GetExportFormat() == StiExportFormat.Pdf)
    {
        StiPdfExportSettings pdfSettings = (StiPdfExportSettings)settings;
        pdfSettings.EmbeddedFonts = true;
        pdfSettings.AllowEditable = StiPdfAllowEditable.No;
        return StiMvcDesignerFx.ExportReportResult(settings);
    }

    return StiMvcDesignerFx.ExportReportResult();
}
...
```
