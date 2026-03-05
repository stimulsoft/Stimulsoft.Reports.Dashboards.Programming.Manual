## WCF Server

When designing a report, a user may process events via the **WCF** server. For this you need to set the **UseWCFService** property to **true**:


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Silverlight.WCFService.UseWCFService = true;
...
```

When the **UseWCFService** property is set to **true**, a user may use the following events:


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Silverlight.WCFService.WCFRenderReport
...
```


The **WCFRenderReport** event occurs when rendering a report;


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Silverlight.WCFService.WCFTestConnection
...
```

The **WCFTestConnection** event occurs when clicking the **Test Connection** button;


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Silverlight.WCFService.WCFBuildObjects
...
```

The **WCFBuildObjects** event occurs when returning the list tables from the created data source;


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Silverlight.WCFService.WCFRetrieveColumns
...
```

The **WCFRetrieveColumns** event occurs when returning the list of data columns for the table;


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Silverlight.WCFService.WCFOpeningReportInDesigner
...
```

The **WCFOpeningReportInDesigner** event occurs when clicking the **Open Report** button in the main menu;


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Engine.GlobalEvents.SavingReportInDesigner
...
```

The **SavingReportInDesigner** event occurs when saving a report;


**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Silverlight.WCFService.WCFExportDocument
...
```

The **WCFExportDocument** event occurs when exporting a report by means of the server. In order to make available a menu with exports in the viewer by means of the server, you must set the **ShowReportSaveToServerButton** property to **true**:

**C#**

```csharp
...
Stimulsoft.Report.StiOptions.Viewer.Elements.ShowReportSaveToServerButton = true;
...
```
