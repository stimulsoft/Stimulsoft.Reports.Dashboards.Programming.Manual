# Showing Reports and Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.


> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `Report.Render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer. Likewise, when using the compilation mode, you need to call the `Report.Compile()` method only if you have actions to perform with the compiled report before it is built and shown in the viewer.

To show a report, you should add the **StiWebViewer** component to the ASPX page and assign a loaded report to it.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    // report.Load(Server.MapPath("Reports/Dashboard.mrt"));
        
    StiWebViewer1.Report = report;
}
...
```


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Viewer.Showing_Reports_1.png)

Also, the **HTML5 Viewer** has a special **OnGetReport** event that you can use to assign a report to the viewer. In this case, you need to load the report in the event handler.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnGetReport="StiWebViewer1_GetReport">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_GetReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    
    e.Report = report;
}
...
```


> **Information**
>
> To assign a report, you should use the specified OnGetReport event. In this case, if the report object is lost for any reason in the cache of the server or session, the client part of the viewer initiates this event, and the report preview will be continued.

If the report is not rendered before showing, the **HTML5 Viewer** component will automatically generate it. So, you can use various types of reports to display the report - report templates, rendered reports, and reports as classes.


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_GetReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = new StiReport();
    report.LoadDocument(Server.MapPath("Reports/SimpleList.mdc"));
    
    e.Report = report;
}
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_GetReport(object sender, StiReportDataEventArgs e)
{
    e.Report = new StiReportCompiledClass();
}
...
```

Since the dashboard is not a static document and requires data to work, the format of the rendered MDC document is not available for it. Instead, it is possible to use a snapshot of the report in the MRT format, which contains all the data necessary for the dashboard to work and can be correctly displayed in the viewer.


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_GetReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/Snapshot.mrt"));
    
    e.Report = report;
}
...
```

### Loading custom fonts

You can load custom fonts using the **StiFontCollection** class, having specified the file that contains a font. To do this, you should call the static method in the constructor to load a font.


**Default.aspx.cs**

```csharp
...
public partial class _Default : Page
{
    static _Default()
    {
        Stimulsoft.Base.StiFontCollection.AddFontFile(Server.MapPath("fonts/my-font/font-name.ttf"));
    }
}
...
```
