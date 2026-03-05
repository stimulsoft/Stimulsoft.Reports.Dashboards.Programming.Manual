# Designer Events

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

**The** **HTML5 Designer** component supports events that allow you to execute necessary operations before specific actions, such as creating and editing report templates, previewing, printing and exporting, interactivity, etc. Below is a sample for processing designer events.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server"
    OnGetReport="StiWebDesigner1_GetReport"
    OnCreateReport="StiWebDesigner1_CreateReport"
    OnSaveReport="StiWebDesigner1_SaveReport">
</cc1:StiWebDesigner>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesigner1_GetReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    
    e.Report = report;
}

protected void StiWebDesigner1_CreateReport(object sender, StiReportDataEventArgs e)
{
    DataSet data = new DataSet();
    data.ReadXmlSchema(Server.MapPath("Data/Demo.xsd"));
    data.ReadXml(Server.MapPath("Data/Demo.xml"));
    
    e.Report.RegData(data);
    e.Report.Dictionary.Synchronize();
}

protected void StiWebDesigner1_SaveReport(object sender, StiReportDataEventArgs e)
{
    try
    {
        e.Report.Save(Server.MapPath("Reports/" + e.Report.ReportName + ".mrt"));
    }
    catch (Exception ex)
    {
        e.ErrorString = ex.Message;
    }
}
...
```

### Events

| **Name** | **Description** |
| --- | --- |
| OnGetReport | The event occurs when [requesting a report for editing](Add_Designer.md). |
| OnCreateReport | The event occurs when [creating new reports](Creating_Report.md) from the designer menu. |
| OnOpenReport | The event occurs when you open a report from the designer menu. In the arguments of the event, the loaded report will be sent. |
| OnPreviewReport | The event occurs when [going to the preview tab](Preview.md), and when interactive activities such as using report variables, dynamic collapsing, drill-down, and sorting a report when previewing it. |
| OnSaveReport | The event occurs when [clicking the Save button](Save_Report.md) on the panel or from the main menu of the designer. |
| OnSaveReportAs | The event occurs when [clicking the Save As button](Save_Report.md) from the main menu of the designer. If the event is not specified, the report will be saved to the local disk. |
| OnExportReport | The event occurs when [exporting reports](Additional_Functionality_of_Preview.md). |
| OnExportReportResponse | The event occurs when [after exporting reports](Additional_Functionality_of_Preview.md) before saving the exported report file. |
| OnExit | The event occurs when [clicking the Exit button](Additional_Functionality_of_Preview.md) in the main menu of the designer. |
