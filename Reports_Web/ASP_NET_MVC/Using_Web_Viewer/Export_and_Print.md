# Export and Printing from Code

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **HTML5 Viewer** provides the ability to print reports in various ways and export reports to various formats. These actions are performed using the viewer menu. If you want to print or export a report by using the code, for example, in the controller action, you can use the special **StiMvcReportResponse** class. This class contains a set of static methods that allow you to print or export a report from the code, and the report viewer is not required.


**Index.cshtml**

```
...
@Html.ActionLink("Print Report from Code", "PrintReport")
<br />
@Html.ActionLink("Export Report from Code", "ExportReport")
...
```


**HomeController.cs**

```csharp
...
private StiReport LoadSimpleList()
{
    DataSet dataSet = new DataSet();
    dataSet.ReadXml(Server.MapPath("Reports/Demo.xml"));
    
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    report.RegData(dataSet);
    
    return report;
}

public ActionResult PrintReport()
{
    StiReport report = LoadSimpleList();
    
    return StiMvcReportResponse.PrintAsPdf(report);
    //return StiMvcReportResponse.PrintAsHtml(report);
}

public ActionResult ExportReport()
{
    StiReport report = LoadSimpleList();
    
    return StiMvcReportResponse.ResponseAsPdf(report);
    //return StiMvcReportResponse.ResponseAsExcel2007(report);
    //return StiMvcReportResponse.ResponseAsText(report);
    //StiMvcReportResponse.ResponseAsJson(report);
}
...
```

The **StiMvcReportResponse** class contains methods for printing in PDF and HTML formats and methods to export the report in any of the supported formats. As arguments, methods can take various export settings, displaying modes and options for saving received files.
