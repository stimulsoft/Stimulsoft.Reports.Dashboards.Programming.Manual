# Preview

The **Flash Designer** component provides the ability to preview reports. To preview the report, just go to the appropriate tab in the designer window. The report template will be transferred to the server-side, rendered and displayed in the embedded viewer.


![](../../../images/topics/Reports_Web.ASP_NET_Core.Using_Web_Flash_Designer.Preview_1.png)

Before previewing the report, it is possible to perform any necessary actions, for example, connect data for the report. To do this, you can use the special **PreviewReport** action that will be called before previewing the report.


**Index.cshtml**

```
...
@Html.StiNetCoreDesignerFx(new StiNetCoreDesignerFxOptions() {
    Actions =
    {
        PreviewReport = "PreviewReport"
    }
})
...
```


**HomeController.cs**

```csharp
...
public IActionResult PreviewReport()
{
    StiReport report = StiNetCoreDesignerFx.GetReportObject(this);
    
    DataSet data = new DataSet("Demo");
    data.ReadXml(StiNetCoreHelper.MapPath(this, "Data/Demo.xml"));
    report.RegData(data);
    
    return StiNetCoreDesignerFx.PreviewReportResult(this, report);
}
...
```
