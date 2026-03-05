## How to Show Report

Put the **StiWebViewerSL** component on a web page. Then you need to use the following code to show a report:


**C#**

```csharp
...
Stimulsoft.Report.StiReport report = new Stimulsoft.Report.StiReport();report.Load("Simple_List.mrt");WebViewerSL1.Report = report;
...
```

If the report was not rendered before showing, then the **WebViewerSL** component renders it automatically. Also the viewer supports loading reports using the Drag&Drop.
