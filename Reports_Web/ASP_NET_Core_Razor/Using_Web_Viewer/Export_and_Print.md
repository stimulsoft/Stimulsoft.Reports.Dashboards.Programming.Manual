# Export and Printing from Code

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **HTML5 Viewer** provides the ability to print reports in various ways and export reports to various formats. These actions are performed using the viewer menu. If you want to print or export a report using the code, for example, in the specific page event, you can use the special **StiNetCoreReportResponse** class. This class contains a set of static methods that allow you to print or export a report from the code, and the report viewer is not required.


**Index.cshtml**

```
page "{handler?}"
...
<a href="PrintReport">Print Report from Code</a>
<br />
<a href="ExportReport">Export Report from Code</a>
...
```


**Index.cshtml.cs**

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

public IActionResult OnGetPrintReport()
{
    StiReport report = LoadSimpleList();
    
    return StiNetCoreReportResponse.PrintAsPdf(report);
    //return StiNetCoreReportResponse.PrintAsHtml(report);
}

public IActionResult OnGetExportReport()
{
    StiReport report = LoadSimpleList();
    
    return StiNetCoreReportResponse.ResponseAsPdf(report);
    //return StiNetCoreReportResponse.ResponseAsExcel2007(report);
    //return StiNetCoreReportResponse.ResponseAsText(report);
    //StiNetCoreReportResponse.ResponseAsJson(report);
}
...
```

The **StiNetCoreReportResponse** class contains methods for printing in PDF and HTML formats and methods to export the report in any of the supported formats. As arguments, methods can take various export settings, displaying modes and options for saving received files.
