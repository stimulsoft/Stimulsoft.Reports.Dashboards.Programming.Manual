# Timeout

When working with the **StiNetCoreViewer** component, you can set the timeout for various operations — [storing the report in the cache](../../ASP_NET_Core/Using_Web_Viewer/Timeout.md#cachetimeout), [server response](../../ASP_NET_Core/Using_Web_Viewer/Timeout.md#requesttimeout), and [query execution](../../ASP_NET_Core/Using_Web_Viewer/Timeout.md#commandtimeout). The timeout setting is done using the component properties and report options.

### CacheTimeout Property

Sets the time in minutes that the server will store the rendered report since the last action of the viewer. The default setting is 10 minutes.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Server.CacheTimeout = 10;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

Using cache will increase the speed of the report viewer. See the chapter [Caching](../../ASP_NET_Core/Using_Web_Viewer/Caching.md) for more information

### RequestTimeout Property

Sets the time to wait for a response from the server in seconds, after which an error will be generated. The default value is 30 seconds. For big reports, it is recommended to increase this value.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Server.RequestTimeout = 30;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

### CommandTimeout Option

Also, for SQL data sources used in the report, you can specify the **Query Timeout** in seconds. The value of this property is stored in the report template for each SQL connection separately.


Below is an example of code that you may use to set the query timeout for the already created connection, and data sources in the report.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Actions.GetReport = "GetReport";
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}

public IActionResult GetReport()
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Report.mrt"));
    ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).CommandTimeout = 1000;
    
    return StiNetCoreViewer.GetReportResult(this, report);
}

public IActionResult ViewerEvent()
{
    return StiNetCoreViewer.ViewerEventResult(this);
}
...
```
