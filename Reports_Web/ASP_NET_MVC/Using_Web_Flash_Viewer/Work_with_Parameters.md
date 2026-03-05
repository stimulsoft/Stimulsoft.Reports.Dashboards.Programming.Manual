# Work with Parameters

To work with report parameters in the **Flash Viewer**, there is a special settings panel. To add a parameter to the panel you need to define a variable in a report, requested by the user. When viewing a report in the viewer such a variable will be automatically added to the settings panel. It supports all types of report variables (normal variables, date and time, borders, lists, etc.).


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Flash_Viewer.Work_with_Parameters_1.png)

To work with report parameters, no additional viewer settings are required. When you assign parameters, the **GetReportSnapshot** action will be called. In this action, the required report template should be loaded again. The required parameters passed from the client-side will be automatically applied to the report when the response is generated.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewerFx("MvcViewerFx1", 
    new StiMvcViewerFxOptions() {
        Actions =
        {
            GetReportSnapshot = "GetReportSnapshot"
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult GetReportSnapshot()
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("~/Content/ReportWithParameters.mrt"));
    
    return StiMvcViewerFx.GetReportSnapshotResult(report);
}
...
```

When working with parameters is not required, you can disable this feature. For this, you can use the **ShowParametersButton** property. Set this property to **false** in this case.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewerFx("MvcViewerFx1", 
    new StiMvcViewerFxOptions() {
        Toolbar =
        {
            ShowParametersButton = false
        }
})
...
```


> **Information**
>
> With this configuration of the viewer, the Parameters panel will not be displayed, even if the parameters are present in the report.
