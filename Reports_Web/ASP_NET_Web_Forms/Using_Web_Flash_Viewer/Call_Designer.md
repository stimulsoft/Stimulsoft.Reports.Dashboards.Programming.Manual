# Calling Designer from Viewer

The **Flash Viewer** component has the ability to call the report designer. The special **Design** button in the toolbar of the viewer (the button is disabled by default) should be used. To use this feature, you should set the **ShowDesignButton** property to **true**, and also to define the **OnDesignReport** event handler.


**Default.aspx**

```
...
<cc1:StiWebViewerFx ID="StiWebViewerFx1" runat="server"
    ShowDesignButton="true"
    OnDesignReport="StiWebViewerFx1_DesignReport">
</cc1:StiWebViewerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewerFx1_DesignReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = e.Report;
    this.Response.Redirect("Designer.aspx?report=" + report.ReportName);
}
...
```


> **Information**
>
> The viewer does not run the designer itself, it only calls the specified event and passes the previewed report as arguments. In the event, you can set redirection to the ASPX page, on which the report designer is placed.
