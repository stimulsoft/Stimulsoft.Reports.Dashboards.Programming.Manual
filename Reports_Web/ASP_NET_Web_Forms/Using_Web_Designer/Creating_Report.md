# Creating New Reports and New Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To run the designer with a new (empty) report, no action is required. When the component is loaded, the new report will be created automatically. If necessary, you can create a new report object, preload the data, or perform other necessary actions.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server"
    OnGetReport="StiWebDesigner1_GetReport">
</cc1:StiWebDesigner>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesigner1_GetReport(object sender, StiReportDataEventArgs e)
{
    e.Report = new StiReport();
    //var newDashboard = StiReport.CreateNewDashboard();
}
...
```

You can also create a new report using the main menu of the designer. The **OnCreateReport** event is used to load data for a new report or perform other necessary actions. This event will be called when you create a new empty report or a report using the wizard.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server"
    OnCreateReport="StiWebDesigner1_CreateReport">
</cc1:StiWebDesigner>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesigner1_CreateReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = new StiReport();
    //var newDashboard = StiReport.CreateNewDashboard();

    // Register data for the new report, if necessary
    DataSet data = new DataSet("Demo");
    data.ReadXml(Server.MapPath("Data/Demo.xml"));
    report.RegData(data);
    //newDashboard.RegData(data);
    report.Dictionary.Synchronize();
    //newDashboard.Dictionary.Synchronize();
    
    e.Report = report;
    //e.Report = newDashboard;
}
...
```
