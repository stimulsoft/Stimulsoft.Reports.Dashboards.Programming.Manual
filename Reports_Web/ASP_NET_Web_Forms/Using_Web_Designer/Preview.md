# Preview

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **HTML5 Designer** component provides the ability to preview reports. To preview the report, just go to the appropriate tab in the designer window. The report template will be transferred to the server-side, rendered, and displayed in the embedded viewer.


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Designer.Preview_1.png)

Before previewing the report, it is possible to perform any necessary actions, for example, connect data for the report. To do this, you can use a special **OnPreviewReport** event which will be called before previewing the report. In the arguments of the event, there will be a report to be previewed. The **OnPreviewReport** event is called before preparing and rendering a report for viewing till its saving to the cash.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server"
    OnPreviewReport="StiWebDesigner1_PreviewReport">
</cc1:StiWebDesigner>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesigner1_PreviewReport(object sender, StiReportDataEventArgs e)
{
    DataSet data = new DataSet("Demo");
    data.ReadXml(Server.MapPath("Data/Demo.xml"));
    e.Report.RegData(data);
}
...
```

If you need to take actions on your report immediately before displaying the report, you can use the **OnGetPreviewReport** event, which is called after the request of the prepared report from the cash.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server"
    OnGetPreviewReport="StiWebDesigner1_GetPreviewReport">
</cc1:StiWebDesigner>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesigner1_GetPreviewReport(object sender, StiReportDataEventArgs e)
{
    DataSet data = new DataSet("Demo");
    data.ReadXml(Server.MapPath("Data/Demo.xml"));
    e.Report.RegData(data);
    
    //report.IsRendered = false;
}
...
```


> **Information**
>
> So as in this event, a prepared report for viewing is transferred. If you need to render again, you should set the **report.IsRendered = false** flag.
