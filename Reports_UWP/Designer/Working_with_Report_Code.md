# Working with Report Code

In this topic we will review the examples of working from code for the report designer **UWP**.


* **Loading a report:**


In order to load the report designer for further editing it is necessary to assign a report to the Report property of the designer. If you do not assign anything to this property, the designer will be loaded


**C#**

```csharp
...
var file = await Windows.Storage.KnownFolders.DocumentsLibrary.GetFileAsync("report.mrt");
var report = new StiReport();
await report.LoadAsync(file);
...
```

Loading a created report (**MDC** file):


**C#**

```csharp
...
var file = await Windows.Storage.Known Folders.DocumentsLibrary.GetFileAsync("report.mdc");
var report = new StiReport();
await report.LoadDocumentAsync(file);
...
```

* **Saving a report:**


After creating or editing a report template you should save the changes. Below is a method of saving a report code in the *.**mrt** file:


**C#**

```csharp
...
var file = await Windows.Storage.KnownFolders.DocumentsLibrary.CreateFileAsync("report.mrt", CreationCollisionOption.ReplaceExisting);
var report = new StiReport();
await report.SaveAsync(file);
...
```

Saving a created report (**MDC** file):


**C#**

```csharp
...
var file = await Windows.Storage.KnownFolders.DocumentsLibrary.CreateFileAsync("report.mdc", CreationCollisionOption.ReplaceExisting);
var report = new StiReport();
await report.SaveDocumentAsync(file);
...
```
