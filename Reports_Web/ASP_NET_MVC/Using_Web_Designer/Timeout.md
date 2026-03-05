# Timeout

When working with the **StiMvcDesigner** component, you can set the timeout for various operations — [storing the report in the cache](#cachetimeout), [server response](#requesttimeout), and [query execution](#commandtimeout). The timeout setting is done using the component properties and report options.

### CacheTimeout Property

Sets the time in minutes that the server will store the rendered report since the last action of the viewer. The default setting is 10 minutes.


**Index.cshtml**

```
...@Html.Stimulsoft().StiMvcDesigner("MvcDesigner1", 
    new StiMvcDesignerOptions() {
        Server =
        {
            CacheTimeout = 10
        }
})
...
```

Using cache will increase the speed of the report designer. See the chapter [Caching](Caching.md) for more information

### RequestTimeout Property

Sets the time to wait for a response from the server in seconds, after which an error will be generated. The default value is 30 seconds. For big reports, it is recommended to increase this value.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesigner("MvcDesigner1", 
    new StiMvcDesignerOptions() {
        Server =
        {
            RequestTimeout = 30
        }
})
...
```

### CommandTimeout Option

Also, for SQL data sources used in the report, you can specify the **Query Timeout** in seconds. The value of this property is stored in the report template for each SQL connection separately.


Below is an example of code that you may use to set the query timeout for the already created connection and data sources in the report.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesigner("MvcDesigner1", 
    new StiMvcDesignerOptions() {
        Actions =
        {
            GetReport = "GetReport",
            DesignerEvent = "DesignerEvent"
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult GetReport()
{ 
    
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Report.mrt"));
    ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).CommandTimeout = 1000;
    
    return StiMvcDesigner.GetReportResult(report);
}

public ActionResult DesignerEvent()
{
    return StiMvcDesigner.DesignerEventResult();
}
...
```
