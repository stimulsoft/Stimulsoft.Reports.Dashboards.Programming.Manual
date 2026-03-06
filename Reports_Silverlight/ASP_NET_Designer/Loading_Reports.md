## Loading Reports

One of the following methods can be used to load a report to the **Web designer**:

* Loading a report before loading the designer;

* Loading a report after loading the designer;

* Loading a report from the main menu of the designer.


* **Loading a report before loading the designer**. In this way the report (for example, from a file) is loaded first and then the designer is loaded. The previously loaded report is specified as a parameter of a method of calling the designer. A code below is a sample for loading a report before loading the designer:


**C#**

```csharp
...
protected void Button1_Click(object sender, EventArgs e)
{
    StiReport report = new StiReport();
    report.Load("D:\\SimpleList.mrt");
    StiWebDesignerSL1.Design(report);
}
...
```

or, as a way, the previously loaded report is assigned to the designer. In this case designer loading is done with this report. See the code below:


**C#**

```csharp
...
protected void Button1_Click(object sender, EventArgs e)
{
    StiReport report = new StiReport();
    report.Load("D:\\SimpleList.mrt");
    StiWebDesignerSL1.Report = report;
    StiWebDesignerSL1.Design();
}
...
```

* **Loading a report after loading the designer** is done using the **GetReport** event. After adding the handler to this event, it will occur each time when a report is required for the designer. In other words, after loading the Web designer requests a report from the server and, if the handler is added to the **GetReport** event, then in this event a report can be assigned to the designer. See the code below how to use the **GetReport** event:

**C#**

```csharp
...
protected void StiWebDesignerSL1_GetReport(object sender, StiWebDesignerSL.StiGetReportEventArgs e)
{
    StiReport report = new StiReport();
    report.Load("D:\\SimpleList.mrt");
    e.Report = report;
}
...
```


* **Loading a report from the main menu of the designer**. A report can be loaded by selecting the **Open Report** menu item. After selecting this menu item the dialog box for specifying a report for loading will appear. Also the designer supports loading reports and other report items (for example, images) using **Drag&Drop**.
