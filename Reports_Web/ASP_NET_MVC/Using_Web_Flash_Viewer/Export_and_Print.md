# Exporting and Printing Reports from Code

The **Flash Viewer** component provides the ability to print the report in various ways and export the report to various formats. These actions are performed using the viewer menu. If you want to print a report or export it using code, for example, in a specific controller action, you can use the special **StiMvcReportResponse** class. This class contains a set of static methods that allow you to print or export a report from the code but you do not need a report viewer.


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
}
...
```

The **StiMvcReportResponse** class contains printing methods to PDF and HTML formats, as well as methods for exporting the report to any of the supported formats. As arguments, methods can take different export settings, display modes and options for saving files.
