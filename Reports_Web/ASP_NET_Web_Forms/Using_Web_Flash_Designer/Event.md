# Designer Events

**The** **Flash Designer** component supports events which allows you to execute necessary operations before certain actions, such as creating and editing report templates, previewing, printing and exporting, sending reports by email, interactivity etc. Below is a sample for processing designer events.


**Default.aspx**

```
...
<cc1:StiWebDesignerFx ID="StiWebDesignerFx1" runat="server"
    OnGetReport="StiWebDesignerFx1_GetReport"
    OnSaveReport="StiWebDesignerFx1_SaveReport">
</cc1:StiWebDesignerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesignerFx1_GetReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    
    e.Report = report;
}

protected void StiWebDesignerFx1_SaveReport(object sender, StiReportDataEventArgs e)
{
    try
    {
        e.Report.Save(Server.MapPath("Reports/" + e.Report.ReportName + ".mrt"));
        e.ErrorCode = 0;
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
| OnGetReport | Occurs when [requesting report for editing](Editing_Report.md). |
| OnCreateReport | Occurs when [creating new reports](Creating_Report.md) from the designer menu. |
| OnPreviewReport | Occurs when [going to the preview tab](Preview.md), as well as when interactive activities such as using report variables, dynamic collapsing, drill-down, and sorting a report when previewing it. |
| OnSaveReport | Occurs when [clicking the Save button](Save_Report.md) on the panel or from the main menu of the designer. |
| OnSaveReportAs | Occurs when [clicking the Save As button](Save_Report.md) from the main menu of the designer. If the event is not specified, the report will be saved to the local disk. |
| OnPrintReport | Occurs when [printing reports](Additional_Functionality_of_Preview.md) in the PDF format. |
| OnExportReport | Occurs when [expoting reports](Additional_Functionality_of_Preview.md). |
| OnExportReportResponse | Occurs when [after exporting reports](Additional_Functionality_of_Preview.md) before saving the exported report file. |
| OnEmailReport | Occurs when sending the report by edmail. |
| OnExit | Occurs when [clicking the Exit button](Additional_Functionality_of_Preview.md) in the main menu of the designer. |
