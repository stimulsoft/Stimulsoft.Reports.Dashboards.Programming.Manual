# Additional Methods

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

For **HTML5 Designer**, there are several additional methods that are used to get the object of the currently edited report, parameters of the current state of the designer and other useful data. These methods can be used in any actions of the designer.


### The GetReportObject() Method

Returns the report object with which the designer is currently working. It is possible to perform the necessary actions with it - register new data sets, change report properties, assign parameters or load another report to the object. Then, the report can be returned to the designer, specifying it as a parameter in the resulting action method.


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostExportReport()
{
    StiReport report = StiNetCoreDesigner.GetReportObject(this);
    report.ReportName = "MyReportName";
    
    return StiNetCoreDesigner.ExportReportResult(this, report);
}
...
```


### The GetActionReportObject() method

Returns the report object that will be used for the particular action. For example, for the **OpenReport** action, this method returns a report loaded from the local disk of the computer. For the **PreviewReport** action, the method returns a prepared copy of the report for preview.


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostOpenReport()
{
    StiReport report = StiNetCoreDesigner.GetActionReportObject(this);
    
    // Register data for the opened report, if necessary
    DataSet data = new DataSet("Demo");
    data.ReadXml(StiNetCoreHelper.MapPath(this, "Data/Demo.xml"));
    report.RegData(data);
    report.Dictionary.Synchronize();
    
    return StiNetCoreDesigner.GetReportResult(this, report);
}
...
```


### The GetFormValues() method

Returns the values of the form that initiated (opened by the POST request) a page of the designer. Thus, it is possible to get a collection of form parameters in any action of the designer.


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostDesignerInteraction()
{
    NameValueCollection formValues = StiNetCoreDesigner.GetFormValues(this);
    
    return StiNetCoreDesigner.InteractionResult(this);
}
...
```

By default, this feature is disabled to optimize requests of the client-side of the designer to the server. To enable it, set the **PassFormValues** property to **true**.


**Index.cshtml**

```
...
@Html.StiNetCoreDesigner(new StiNetCoreDesignerOptions() {
    Server =
    {
        PassFormValues = true
    }
})
...
```


### The GetRequestParams() method

Returns all parameters of the current state of the designer passed to the server side. They can be useful for determining the type of action that the designer is currently executing - for example, to determine the type of export, as well as all action parameters.


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostExportReport()
{
    StiRequestParams requestParams = StiNetCoreDesigner.GetRequestParams(this);
    if (requestParams.ExportFormat == StiExportFormat.Pdf)
    {
        StiReport report = StiNetCoreDesigner.GetReportObject(this);
        
        // Some action with report for the PDF export
        // ...
        
        return StiNetCoreDesigner.ExportReportResult(this, report);
    }
    
    return StiNetCoreDesigner.ExportReportResult(this);
}
...
```


### The GetExportSettings() method

Returns all parameters of the current report export. The type of the parameter object will correspond to the type of export selected in the report preview menu. Any export parameters can be changed and passed to the input of the resulting method. In this case, the report will be exported with the parameters transferred.


**Index.cshtml.cs**

```csharp
...
public IActionResult OnPostExportReport()
{
    StiExportSettings settings = StiNetCoreDesigner.GetExportSettings(this);
    if (settings.GetExportFormat() == StiExportFormat.Pdf)
    {
        StiPdfExportSettings pdfSettings = (StiPdfExportSettings)settings;
        pdfSettings.EmbeddedFonts = true;
        pdfSettings.AllowEditable = StiPdfAllowEditable.No;
        return StiNetCoreDesigner.ExportReportResult(this, settings);
    }
    
    return StiNetCoreDesigner.ExportReportResult(this);
}
...
```


### The MapPath() and MapWebRootPath() methods

**Returns the absolute path, respectively, to the application or wwwroot directory. You can use this to upload report templates files, data files, etc. These methods are located in the StiNetCoreHelper static class.

                Index.cshtml.cs

                ...
                public IActionResult OnPostGetReport()
                {
                StiReport report = new StiReport();
                report.Load(StiNetCoreHelper.MapPath(this, "Reports/SimpleList.mrt"));
                
                return StiNetCoreDesigner.GetReportResult(this, report);
                }
                ...**
