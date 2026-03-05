## Deployment Reports as Files


The most frequently used way of reports deployment is deployment reports as files. Stimulsoft Reports supports two type of files: unpacked report (the .mrt file extension) and packed reports (the .mrz file extension). Packed reports have small file size but it takes much time for saving and loading them. For loading the previously saved report the following code is required:


C#:

```
StiReport report = new StiReport();
report.Load("report.mrt");
```


VB.NET:

```
Dim Report As StiReport = New StiReport()
Report.Load("report.mrt") 
```


For saving the report the following will be needed:


C#:

```
StiReport report = new StiReport();
report.Save("report.mrt");
```


VB.NET:

```
Dim Report As StiReport = New StiReport()
Report.Save("report.mrt") 
```
