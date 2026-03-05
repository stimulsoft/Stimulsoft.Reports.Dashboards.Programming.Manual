# Creating New Reports

To run the designer with a new (empty) report, it is enough to create a new report object and send it to the designer using any of the available methods. If necessary, you can load the data for the report, or perform any other necessary actions.


**Default.aspx**

```
...
<cc1:StiWebDesignerFx ID="StiWebDesignerFx1" runat="server"
    OnGetReport="StiWebDesignerFx1_GetReport">
</cc1:StiWebDesignerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesignerFx1_GetReport(object sender, StiReportDataEventArgs e)
{
    e.Report = new StiReport();
}
...
```

You can also create a new report using the main menu of the designer. The **OnCreateReport** event is used to load data for a new report, or to perform some other necessary actions. This event will be called when you create a new empty report, or when you create a report using the wizard.


**Default.aspx**

```
...
<cc1:StiWebDesignerFx ID="StiWebDesignerFx1" runat="server"
    OnCreateReport="StiWebDesignerFx1_CreateReport">
</cc1:StiWebDesignerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebDesignerFx1_CreateReport(object sender, StiReportDataEventArgs e)
{
    StiReport report = new StiReport();
    
    // Register data for the new report, if necessary
    DataSet data = new DataSet("Demo");
    data.ReadXml(Server.MapPath("Data/Demo.xml"));
    report.RegData(data);
    report.Dictionary.Synchronize();
    
    e.Report = report;
}
...
```
