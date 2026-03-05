# Export and Printing Reports from Code

**Flash Viewer** provides the ability to print reports in various ways and export reports to various formats. These actions are performed using the viewer menu. If you want to print or export the report by using the code, for example, in the event of pressing the button, you can use the special **StiReportResponse** class. This class contains a set of static methods that allow you to print or export a report from the code, and the report viewer is not required.


**Default.aspx**

```
...
<asp:Button ID="Button1" runat="server" onclick="Button1_Click" Text="Print Report" />
<asp:Button ID="Button2" runat="server" onclick="Button2_Click" Text="Export Report" />
...
```


**Default.aspx.cs**

```csharp
...
private StiReport LoadSimpleList()
{
    DataSet dataSet = new DataSet();
    dataSet.ReadXml(Server.MapPath("Reports/Demo.xml"));
    
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    report.RegData(dataSet);
    
    return report;
}

protected void Button1_Click(object sender, EventArgs e)
{
    StiReport report = LoadSimpleList();
    
    StiReportResponse.PrintAsPdf(report);
    //StiReportResponse.PrintAsHtml(report);
}

protected void Button2_Click(object sender, EventArgs e)
{
    StiReport report = LoadSimpleList();
    
    StiReportResponse.ResponseAsPdf(report);
    //StiReportResponse.ResponseAsExcel2007(report);
    //StiReportResponse.ResponseAsText(report);
}
...
```

The **StiReportResponse** class contains methods for printing in PDF and HTML formats, as well as methods to export the report in any of the supported formats. As arguments, methods can take various export settings, displaying modes and options for saving received files.
