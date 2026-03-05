## How to Show Report

> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `Report.Render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer. Likewise, when using the compilation mode, you need to call the `Report.Compile()` method only if you have actions to perform with the compiled report before it is built and shown in the viewer.

Just call only one method to show a report:


**C#**

```csharp
...
StiReport report = new StiReport();
report.Load("report.mrt");
report.Show();
...
```


**VB.NET**

```vbnet
...
Dim Report As StiReport = New StiReport()
Report.Load("report.mrt")
Report.Show()
...
```

If the report was not rendered before showing, the **Show** method will render a report using the **Render** method.
