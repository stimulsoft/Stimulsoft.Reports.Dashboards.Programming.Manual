# Additional Methods

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

For **HTML5 Viewer**, several additional methods are used to get the object of the currently viewed report, parameters of the viewer's current state, and other useful data. These methods can be used in any actions of the viewer.


### The GetReportObject() method

Returns the report object with which the viewer is currently working. It is possible to perform the necessary actions with it - register new data sets, change report properties, assign parameters or load another report to the object. Then, the report can be returned to the viewer, specifying it as a parameter in the resulting action method.


**HomeController.cs**

```csharp
...
public ActionResult ViewerInteraction()
{
    StiReport report = StiMvcViewer.GetReportObject();
    report.ReportName = "MyReportName";
    
    return StiMvcViewer.InteractionResult(report);
}
...
```


### The GetRouteValues() method

Returns values for URLs with which the viewer page was opened. Thus, it is possible to get the initial collection of run page parameters in any viewer action and use these values for any checks and conditions.


**HomeController.cs**

```csharp
...
public ActionResult ViewerInteraction()
{
    RouteValueDictionary routeValues = StiMvcViewer.GetRouteValues();
    
    return StiMvcViewer.InteractionResult();
}
...
```

You can also get values of URL parameters by parameter name, specifying it as the parameter of the called action of the viewer.


**HomeController.cs**

```csharp
...
public ActionResult ViewerInteraction(string id)
{
    return StiMvcViewer.InteractionResult();
}
...
```


### The GetFormValues() method

Returns the values of the form that initiated (opened by the POST request) a page of the viewer. Thus, it is possible to get a collection of form parameters in any action of the viewer.


**HomeController.cs**

```csharp
...
public ActionResult ViewerInteraction()
{
    NameValueCollection formValues = StiMvcViewer.GetFormValues();
    
    return StiMvcViewer.InteractionResult();
}
...
```

By default, this feature is disabled to optimize requests of the client-side of the viewer to the server. To enable it, set the **PassFormValues** property to **true**.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Server =
        {
            PassFormValues = true
        }
})
...
```


### The GetRequestParams() method

Returns all parameters of the current state of the viewer passed to the server-side. They can be useful for determining the type of action that the viewer is currently executing - for example, to determine the type of export, and all action parameters.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiRequestParams requestParams = StiMvcViewer.GetRequestParams();
    if (requestParams.ExportFormat == StiExportFormat.Pdf)
    {
        StiReport report = StiMvcViewer.GetReportObject();
        
        // Some action with report for the PDF export
        // ...

        return StiMvcViewer.ExportReportResult(report);
    }

    return StiMvcViewer.ExportReportResult();
}
...
```


You can change the values of some parameters. After making changes, for the correct operation of the viewer, you should transfer the modified parameter object to the input of the resulting method.


**HomeController.cs**

```csharp
...
public ActionResult ViewerInteraction()
{
    StiRequestParams requestParams = StiMvcViewer.GetRequestParams();
    if (requestParams.Action == StiAction.Variables)
    {
        requestParams.Interaction.Variables["Variable1"] = "MyValue";
        return StiMvcViewer.InteractionResult(requestParams);
    }

    return StiMvcViewer.InteractionResult();
}
...
```


### The GetExportSettings() method

Returns all the parameters of the current report export. The type of the parameter object will correspond to the type of export selected in the viewer menu. Any export parameters can be changed and passed to the input of the resulting method. In this case, the report will be exported with the parameters transferred.


**HomeController.cs**

```csharp
...
public ActionResult ExportReport()
{
    StiExportSettings settings = StiMvcViewer.GetExportSettings();
    if (settings.GetExportFormat() == StiExportFormat.Pdf)
    {
        StiPdfExportSettings pdfSettings = (StiPdfExportSettings)settings;
        pdfSettings.EmbeddedFonts = true;
        pdfSettings.AllowEditable = StiPdfAllowEditable.No;
        return StiMvcViewer.ExportReportResult(settings);
    }

    return StiMvcViewer.ExportReportResult();
}
...
```
