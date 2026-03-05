## Run Designer

For running the Web report designer it is necessary to put non visual **StiWebDesignerSL** component on the form and, in the event handler of a control, to call the **Design()** method:


**ASP.NET**

```
...
<cc1:StiWebDesignerSL ID="StiWebDesignerSL1" runat="server" />
...
```


**C#**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{ 
    StiReport report = new StiReport();
    StiWebDesignerSL1.Report = myReport;
}
...
```

For loading a report in the Web designer, the method of calling can be slightly modified:


**C#**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{
    StiReport report = new StiReport();
    report.Load("D:\\SimpleList.mrt");
    StiWebDesignerSL1.Design(report);
}
...
```
