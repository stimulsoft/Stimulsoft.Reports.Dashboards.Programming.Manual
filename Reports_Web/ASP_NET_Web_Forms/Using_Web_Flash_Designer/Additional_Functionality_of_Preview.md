# Additional Features of Preview

The preview window of the **Flash Designer** component has a fully functional interactive **Flash Viewer** that can print and export reports, supports working with report parameters, interactive reports and sending them via email. To use these features, you do not need any additional settings for the report designer.


In any of the above actions, you can work with the report template, for example, change its properties and parameters, connect new data for rendering.


**Default.aspx**

```
...
<cc1:StiWebDesignerFx ID="StiWebDesignerFx1" runat="server"
    OnExportReport="StiWebDesignerFx1_ExportReport">
</cc1:StiWebDesignerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesignerFx1_ExportReport(object sender, StiReportDataEventArgs e)
{
    e.Report.ReportName = "MyReportName";
    e.Report.ReportAlias = "MyReportAlias";
}
...
```


> **Information**
>
> If you do not need any of these additional options to preview the report (for example, exporting or printing a report), you can disable them using the appropriate properties of the **Flash Designer** component.
