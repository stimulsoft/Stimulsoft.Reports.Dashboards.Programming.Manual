# Exporting Reports and Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **HTML5 Viewer** component allows you to export the displayed report to three dozen various formats, such as **PDF**, **HTML**, **Word**, **Excel**, **XPS**, **RTF**, **images**, **text**, and others. Export functions do not require additional settings for the viewer. You may export the dashboard to PDF, Excel, image files.


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Viewer.Export_1.png)

### Export Events

To perform any actions, a special **OnExportReport** event is assigned before the report is exported. In this event, you can get the report export type, get the report itself, get the report export settings, and change them if necessary.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnExportReport="StiWebViewer1_ExportReport">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_ExportReport(object sender, StiExportReportEventArgs e)
{
    StiExportFormat format = e.Format;
    StiReport report = e.Report;
    StiExportSettings settings = e.Settings;
}
...
```

To perform any actions with an already exported report, the **OnExportReportResponse** event is used. This event will be called immediately before the file is saved. In this event, you can get the export format, the type of the Web content, and the name of the file to save. You can also get and, if necessary, change the byte stream of the final export file.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnExportReportResponse="StiWebViewer1_ExportReportResponse">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_ExportReportResponse(object sender, StiExportReportResponseEventArgs e)
{
    StiExportFormat format = e.Format;
    string contentType = e.ContentType;
    string fileName = e.FileName;
    Stream stream = e.Stream;
}
...
```


### Export Settings

Each report export format of the **HTML5 Viewer** component has a lot of settings, and each setting has its default values. Sometimes you need to set other default values. For this purpose, a special **DefaultExportSettings** property of the viewer is used. It is a container for all the default export settings.


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{
    StiWebViewer1.DefaultExportSettings.ExportToPdf.ImageQuality = 0.75f;
    StiWebViewer1.DefaultExportSettings.ExportToPdf.ImageFormat = StiImageFormat.Color;
    StiWebViewer1.DefaultExportSettings.ExportToHtml.ExportMode = StiHtmlExportMode.Div;
}
...
```

When calling the required export through the Viewer menu, the Export Settings dialog box will be displayed. The values of the dialog box items will match the default export settings. If you change the settings in the dialog box and confirm the export of the report, the settings will be saved in the browser cookies, and upon the subsequent call, the export will be restored. The viewer allows you to disable saving the export settings if you always want to restore the default settings. To do this, just set the value of the **StoreExportSettings** property to **false**.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    StoreExportSettings="false">
</cc1:StiWebViewer>
...
```

Also, if required, you can completely hide export dialogs. Exporting will always be done with default settings. For this, it is enough to set the value of the **ShowExportDialog** property to **false**.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    ShowExportDialog="false">
</cc1:StiWebViewer>
...
```

The **HTML5 Viewer** component contains 30+ export formats, and sometimes you need to disable unwanted formats. This allows you to simplify UI and the use of the viewer. To disable unused export formats, it is enough to set the values for the corresponding properties of the viewer listed in the list below to **false**.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    ShowExportToDocument="true"
    ShowExportToPdf="true"
    ShowExportToXps="true"
    ShowExportToPowerPoint="true"
    ShowExportToHtml="true"
    ShowExportToHtml5="true"
    ShowExportToMht="true"
    ShowExportToText="true"
    ShowExportToRtf="true"
    ShowExportToWord2007="true"
    ShowExportToOpenDocumentWriter="true"
    ShowExportToExcel="true"
    ShowExportToExcelXml="true"
    ShowExportToExcel2007="true"
    ShowExportToOpenDocumentCalc="true"
    ShowExportToCsv="true"
    ShowExportToDbf="true"
    ShowExportToXml="true"
    ShowExportToDif="true"
    ShowExportToSylk="true"
    ShowExportToImageBmp="true"
    ShowExportToImageGif="true"
    ShowExportToImageJpeg="true"
    ShowExportToImagePcx="true"
    ShowExportToImagePng="true"
    ShowExportToImageTiff="true"
    ShowExportToImageMetafile="true"
    ShowExportToImageSvg="true"
    ShowExportToImageSvgz="true">
</cc1:StiWebViewer>
...
```

The **HTML5 Viewer** component can completely disable the export menu. To do this, set the value of the **ShowSaveButton** property to **false**.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    ShowSaveButton="false">
</cc1:StiWebViewer>
...
```
