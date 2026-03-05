## Standalone Reports


It is required to use the program code to compile standalone reports. It is impossible to create standalone reports using the designer. The following code will create the standalone report:


C#:

```
StiReport report = new StiReport();
report.Load("report.mrt");
report.CompileStandaloneReport("report.exe", StiStandaloneReportType.Show);
```


VB.NET:

```
Dim Report As New StiReport()
Report.Load("report.mrt")
Report.CompileStandaloneReport("report.exe", StiStandaloneReportType.Show)
```


It is important to remember that for working with standalone reports the Stimulsoft Reports libraries are required. Besides, the report should get all data itself.
