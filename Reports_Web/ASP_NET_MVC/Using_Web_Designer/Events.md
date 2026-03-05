# Additional Methods

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

For **HTML5 Designer**, several additional methods are used to get the object of the currently edited report, parameters of the current state of the designer, and other useful data. These methods can be used in any actions of the designer.


### The GetReportObject() Method

Returns the report object with which the designer is currently working. It is possible to perform the necessary actions - register new data sets, change report properties, assign parameters or load another report to the object. Then, the report can be returned to the designer, specifying it as a parameter in the resulting action method.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiReport report = StiMvcDesigner.GetReportObject();
    report.ReportName = "MyReportName";
    
    return StiMvcDesigner.ExportReportResult(report);
}
...
```


### The GetActionReportObject() method

Returns the report object that will be used for the particular action. For example, for the **OpenReport** action, this method returns a report loaded from the local disk of the computer. For the **PreviewReport** action, the method returns a prepared copy of the report for preview.


**HomeController.cs**

```csharp
...
public ActionResult OpenReport()
{
    StiReport report = StiMvcDesigner.GetActionReportObject();
    
    // Register data for the opened report, if necessary
    DataSet data = new DataSet("Demo");
    data.ReadXml(Server.MapPath("~/Content/Data/Demo.xml"));
    report.RegData(data);
    report.Dictionary.Synchronize();
    
    return StiMvcDesigner.GetReportResult(report);
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
    RouteValueDictionary routeValues = StiMvcDesigner.GetRouteValues();
    
    return StiMvcDesigner.ExportReportResult();
}
...
```

You can also get values of URL parameters by parameter name, specifying it as the parameter of the called action of the designer.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport(string id)
{
    return StiMvcDesigner.ExportReportResult();
}
...
```


### The GetRequestParams() method

Returns all parameters of the current state of the designer passed to the server-side. They can be useful for determining the type of action that the designer is currently executing - for example, to determine the type of export, and all action parameters.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiRequestParams requestParams = StiMvcDesigner.GetRequestParams();
    if (requestParams.ExportFormat == StiExportFormat.Pdf)
    {
        StiReport report = StiMvcDesigner.GetReportObject();
        
        // Some action with report for the PDF export
        // ...
        
        return StiMvcDesigner.ExportReportResult(report);
    }
    
    return StiMvcDesigner.ExportReportResult();
}
...
```


### The GetExportSettings() method

Returns all parameters of the current report export. The parameter object type will correspond to the type of export selected in the report preview menu. Any export parameters can be changed and passed to the input of the resulting method. In this case, the report will be exported with the parameters transferred.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiExportSettings settings = StiMvcDesigner.GetExportSettings();
    if (settings.GetExportFormat() == StiExportFormat.Pdf)
    {
        StiPdfExportSettings pdfSettings = (StiPdfExportSettings)settings;
        pdfSettings.EmbeddedFonts = true;
        pdfSettings.AllowEditable = StiPdfAllowEditable.No;
        return StiMvcDesigner.ExportReportResult(settings);
    }
    
    return StiMvcDesigner.ExportReportResult();
}
...
```
