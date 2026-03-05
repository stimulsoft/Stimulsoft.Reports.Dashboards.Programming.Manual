# Exporting Reports

The **Angular Viewer** component allows you to export the displayed report to three dozen of various formats, such as **PDF**, **HTML**, **Word**, **Excel**, **XPS**, **RTF**, images, text and others.


![](../../../images/topics/Reports_Web.Angular.Using_Web_Viewer.Export_1.png)

The export function does not require additional settings for the viewer. If you need to perform any actions before exporting the report, you can define a special **ExportReport** action.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Actions.ExportReport = "ExportReport";
            
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}

public IActionResult ExportReport()
{
    // Some code before export
    // ...
    
    return StiAngularViewer.ExportReportResult(this);
}
...
```

### Export settings

Each report export format of the **Angular Viewer** component has a lot of settings, and each setting has its own default values. Sometimes you need to set other default values. For this purpose, a special **DefaultSettings** property of the viewer is used. It is a container for all the default export settings.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Exports.DefaultSettings.ExportToPdf.ImageQuality = 0.75f;
    options.Exports.DefaultSettings.ExportToPdf.ImageFormat = Stimulsoft.Report.Export.StiImageFormat.Color;
    options.Exports.DefaultSettings.ExportToHtml.ExportMode = Stimulsoft.Report.Export.StiHtmlExportMode.Div;
    options.Exports.DefaultSettings.ExportToHtml.UseEmbeddedImages = true;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

If it is required, you can completely hide export dialogs. Exporting will always be done with default settings. For this, it is enough to set the value of the **ShowExportDialog** property to **false**.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Exports.ShowExportDialog = false;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

The **Angular Viewer** component contains 30+ export formats, and sometimes you need to disable unwanted formats. This allows you to simplify UI and the use of the viewer. To disable unused export formats, it is enough to set the values for the corresponding properties of the viewer listed in the list below to **false**.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Exports.ShowExportToDocument = true;
    options.Exports.ShowExportToPdf = true;
    options.Exports.ShowExportToXps = true;
    options.Exports.ShowExportToPowerPoint = true;
    options.Exports.ShowExportToHtml = true;
    options.Exports.ShowExportToHtml5 = true;
    options.Exports.ShowExportToMht = true;
    options.Exports.ShowExportToText = true;
    options.Exports.ShowExportToRtf = true;
    options.Exports.ShowExportToWord2007 = true;
    options.Exports.ShowExportToOpenDocumentWriter = true;
    options.Exports.ShowExportToExcel = true;
    options.Exports.ShowExportToExcelXml = true;
    options.Exports.ShowExportToExcel2007 = true;
    options.Exports.ShowExportToOpenDocumentCalc = true;
    options.Exports.ShowExportToCsv = true;
    options.Exports.ShowExportToDbf = true;
    options.Exports.ShowExportToXml = true;
    options.Exports.ShowExportToDif = true;
    options.Exports.ShowExportToSylk = true;
    options.Exports.ShowExportToImageBmp = true;
    options.Exports.ShowExportToImageGif = true;
    options.Exports.ShowExportToImageJpeg = true;
    options.Exports.ShowExportToImagePcx = true;
    options.Exports.ShowExportToImagePng = true;
    options.Exports.ShowExportToImageTiff = true;
    options.Exports.ShowExportToImageMetafile = true;
    options.Exports.ShowExportToImageSvg = true;
    options.Exports.ShowExportToImageSvgz = true;   
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

The **Angular Viewer** component can completely disable the export menu. To do this, set the value of the **ShowSaveButton** property to **false**.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Toolbar.ShowSaveButton = false;   
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```
