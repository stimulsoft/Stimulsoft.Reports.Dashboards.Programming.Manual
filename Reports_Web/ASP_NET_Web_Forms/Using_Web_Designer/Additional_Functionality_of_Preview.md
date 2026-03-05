# Additional Features of Preview

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The preview window of the **HTML5 Designer** component has a fully functional interactive HTML5 Viewer that can print and export reports, supports working with report parameters, dynamic sorting, interactive reports, collapsing, etc. To use these features, you do not need any additional settings for the report designer.


In any of the above actions, you can work with the report template, such as changing its properties and parameters and connecting new data for rendering.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server"
    OnExportReport="StiWebDesigner1_ExportReport">
</cc1:StiWebDesigner>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesigner1_ExportReport(object sender, StiReportDataEventArgs e)
{
    e.Report.ReportName = "MyReportName";
    e.Report.ReportAlias = "MyReportAlias";
}
...
```


> **Information**
>
> Suppose you do not need any additional options to preview the report (for example, exporting or printing a report). In that case, you can disable them using the appropriate properties of the **HTML5 Designer** component.
