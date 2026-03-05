# Editing Reports and Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To edit a report template, you need to add the **StiWebDesigner** component to the ASPX page and assign a loaded report template to it.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server">
</cc1:StiWebDesigner>
...
```


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    //report.Load(Server.MapPath("Reports/Dashboard.mrt"));
        
    StiWebDesigner1.Report = report;
}
...
```


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Designer.Add_Designer_1.png)

Also, **HTML5 Designer** has a special **OnGetReport** event that you can use to assign a report template. In this case, you need to load the report in the event handler.


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
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/SimpleList.mrt"));
    
    e.Report = report;
}
...
```


> **Information**
>
> The **OnGetReport** event will be called regardless of whether the report was previously assigned or not. If the report is already assigned to the designer, then, in the event arguments, the **e.Report** property will contain the loaded report object. You can change it or assign a new report.

By default, **HTML5 Designer** uses the entire area of the browser window to edit the report. To display a component in a specific HTML page with the specific position and dimensions, it is enough to set its width and height using the **Width** and **Height** properties.


**Default.aspx**

```
...
<cc1:StiWebDesigner ID="StiWebDesigner1" runat="server"
    Width="1000px" Height="800px">
</cc1:StiWebDesigner>
...
```
