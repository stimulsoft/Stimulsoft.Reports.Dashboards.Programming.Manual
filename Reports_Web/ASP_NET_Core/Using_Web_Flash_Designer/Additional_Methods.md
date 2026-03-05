# Addtional Methods

For **Flash Designer**, there are several additional methods that are used to get the object of the currently edited report, parameters of the current state of the designer and other useful data. These methods can be used in any actions of the designer.


### The GetReportObject() method

Returns the report object with which the designer is currently working. It is possible to perform the necessary actions with it - register new data sets, change report properties, assign parameters or load another report to the object. Then, the report can be returned to the designer, specifying it as a parameter in the resulting action method.


**HomeController.cs**

```csharp
...
public IActionResult ExportReport()
{
    StiReport report = StiNetCoreDesignerFx.GetReportObject(this);
    report.ReportName = "MyReportName";
    
    return StiNetCoreDesignerFx.ExportReportResult(this, report);
}
...
```


### The GetRouteValues() method

Returns values for URLs with which the designer page was opened. Thus, it is possible to get the initial collection of page parameters to run the designer and use these values for any checks and conditions.


**HomeController.cs**

```csharp
...
public IActionResult ExportReport()
{
    RouteValueDictionary routeValues = StiNetCoreDesignerFx.GetRouteValues(this);
    
    return StiNetCoreDesignerFx.ExportReportResult(this);
}
...
```

You can also get values of URL parameters by parameter name, specifying it as the parameter of the called action of the designer.


**HomeController.cs**

```csharp
...
public IActionResult ExportReport(string id)
{
    return StiNetCoreDesignerFx.ExportReportResult(this);
}
...
```


### The GetRequestParams() method

Returns all parameters of the current state of the designer passed to the server-side. They can be useful for determining the type of action that the designer is currently executing - for example, to determine the type of export, as well as all action parameters.


**HomeController.cs**

```csharp
...
public IActionResult ExportReport()
{
    StiRequestParams requestParams = StiNetCoreDesignerFx.GetRequestParams(this);
    if (requestParams.ExportFormat == StiExportFormat.Pdf)
    {
        StiReport report = StiNetCoreDesignerFx.GetReportObject(this);
        
        // Some action with report for the PDF export
        // ...
        
        return StiNetCoreDesignerFx.ExportReportResult(this, report);
    }
    
    return StiNetCoreDesignerFx.ExportReportResult(this);
}
...
```


### The GetLocalizationName() method

Returns the name of the requested XML localization file in the **GetLocalization** action. By default, this value is used when creating a response to the designer. Can be used to manage loading of localization files.


**HomeController.cs**

```csharp
...
public IActionResult GetLocalization()
{
    string name = StiNetCoreDesignerFx.GetLocalizationName(this);
    string path = "Localization/" + name;
    
    return StiNetCoreDesignerFx.GetLocalizationResult(this, path);
}
...
```


### The GetExportSettings() method

Returns all parameters of the current report export. The type of the parameter object will correspond to the type of export selected in the report preview menu. Any export parameters can be changed and passed to the input of the resulting method. In this case, the report will be exported with the parameters transferred.


**HomeController.cs**

```csharp
...
public IActionResult ExportReport()
{
    StiExportSettings settings = StiNetCoreDesignerFx.GetExportSettings(this);
    if (settings.GetExportFormat() == StiExportFormat.Pdf)
    {
        StiPdfExportSettings pdfSettings = (StiPdfExportSettings)settings;
        pdfSettings.EmbeddedFonts = true;
        pdfSettings.AllowEditable = StiPdfAllowEditable.No;
        return StiNetCoreDesignerFx.ExportReportResult(this, settings);
    }

    return StiNetCoreDesignerFx.ExportReportResult(this);
}
...
```


### The MapPath() и MapWebRootPath() methods

**Returns the absolute path, respectively, to the application or wwwroot directory. You can use this to upload report templates files, data files, etc. These methods are located in the StiNetCoreHelper static class.

                HomeController.cs

                ...
                public IActionResult GetReport()
                {
                StiReport report = new StiReport();
                report.Load(StiNetCoreHelper.MapPath(this, "Reports/SimpleList.mrt"));
                
                return StiNetCoreDesignerFx.GetReportResult(this, report);
                }
                ...**
