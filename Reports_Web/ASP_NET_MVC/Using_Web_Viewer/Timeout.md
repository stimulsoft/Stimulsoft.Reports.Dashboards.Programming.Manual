# Timeout

When working with the **StiMvcViewer** component, you can set the timeout for various operations — [storing the report in the cache](#cachetimeout), [server response](#requesttimeout), and [query execution](#commandtimeout). The timeout setting is done using the component properties and report options.

### CacheTimeout Property

Sets the time in minutes that the server will store the rendered report since the last action of the viewer. The default setting is 10 minutes.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Server =
        {
            CacheTimeout = 10
        }
})
...
```

Using the cache will increase the speed of the report viewer. See the chapter [Caching](Caching.md) for more information

### RequestTimeout Property

Sets the time to wait for a response from the server in seconds, after which an error will be generated. The default value is 30 seconds. For big reports, it is recommended to increase this value.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
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
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Actions =
        {
            GetReport = "GetReport",
            ViewerEvent = "ViewerEvent"
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
    
    return StiMvcViewer.GetReportResult(report);
}

public ActionResult ViewerEvent()
{
    return StiMvcViewer.ViewerEventResult();
}
...
```
