# Basic Approaches

After the report has been created you may either save the report as a special basic class (for this you should use the Save as command) or save the report as a regular report and then use it as a master report. In the first case, you will get the C# or VB.NET class, and will be able to create new reports. For example:


**C#**

```csharp
...
Reports.Report master = new Reports.Report();master.RegData(dataSet);master.Design();
...
```

In order to use the basic report when creating a new report in the designer, you need to add the following string of a code:


**C#**

```csharp
...
StiReport.ReportType = typeof(Reports.Report);
...
```

Then all new reports will be automatically inherited from the basic class. In the second way you need to use the following code:


**C#**

```csharp
...
StiReport masterReport = new StiReport();
masterReport.Load("d:\\master-detail.mrt");

StiReport report = new StiReport();
report.RegData(dataSet);

report.MasterReport = masterReport.SaveToString();
report.Design();
...
```
