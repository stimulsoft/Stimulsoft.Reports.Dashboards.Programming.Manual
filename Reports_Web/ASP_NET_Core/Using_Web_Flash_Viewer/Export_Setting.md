# Exporting Reports

The **Flash Viewer** component allows you to export the displayed report in three dozen of various formats, such as **PDF**, **HTML**, **Word**, **Excel**, **XPS**, **RTF**, images, text and others.


![](../../../images/topics/Reports_Web.ASP_NET_Core.Using_Web_Flash_Viewer.Export_Setting_1.png)

The export function does not require additional settings for the viewer. If you need to perform any actions before exporting the report, you can define a special **ExportReport** action.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Actions =
    {
        ExportReport = "ExportReport"
    }
})
...
```


**HomeController.cs**

```csharp
...
public IActionResult ExportReport()
{
    // Some code before export
    // ...
    
    return StiNetCoreViewerFx.ExportReportResult(this);
}
...
```

### Export Settings

The **Flash Viewer** component contains 30+ export formats, and sometimes you need to disable unwanted formats. This allows you to simplify UI and the use of the viewer. To disable unused export formats, it is enough to set the values for the corresponding properties of the viewer listed in the list below to **false**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Exports =
    {
        ShowExportToDocument = true,
        ShowExportToPdf = true,
        ShowExportToXps = true,
        ShowExportToPowerPoint = true,
        ShowExportToHtml = true,
        ShowExportToHtml5 = true,
        ShowExportToMht = true,
        ShowExportToText = true,
        ShowExportToRtf = true,
        ShowExportToWord2007 = true,
        ShowExportToOpenDocumentWriter = true,
        ShowExportToExcel = true,
        ShowExportToExcelXml = true,
        ShowExportToExcel2007 = true,
        ShowExportToOpenDocumentCalc = true,
        ShowExportToCsv = true,
        ShowExportToDbf = true,
        ShowExportToXml = true,
        ShowExportToDif = true,
        ShowExportToSylk = true,
        ShowExportToImageBmp = true,
        ShowExportToImageGif = true,
        ShowExportToImageJpeg = true,
        ShowExportToImagePcx = true,
        ShowExportToImagePng = true,
        ShowExportToImageTiff = true,
        ShowExportToImageMetafile = true,
        ShowExportToImageSvg = true,
        ShowExportToImageSvgz = true
    }
})
...
```

Also, if required, you can completely hide export dialogs. Exporting will always be done with default settings. For this, it is enough to set the value of the **ShowExportDialog** property to **false**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Exports =
    {
        ShowExportDialog = false
    }
})
...
```

The **Flash Viewer** component can completely disable the export menu. To do this, set the value of the **ShowSaveButton** property to **false**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Toolbar =
    {
        ShowSaveButton = false
    }
})
...
```
