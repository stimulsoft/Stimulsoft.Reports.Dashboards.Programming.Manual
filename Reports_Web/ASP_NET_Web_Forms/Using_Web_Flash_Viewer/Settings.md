# Viewer Settings

**Flash Viewer** can be setup using the component properties which can be set on the ASPX page using C#/VB code. Below are samples of using the viewer properties.


**Default.aspx**

```
...
<cc1:StiWebViewerFx ID="StiWebViewerFx1" runat="server"
    ShowPrintButton="false"
    ShowSendEmailButton="true"
    ShowTooltips="false"
    ShowExportToDbf="false"
    ShowExportToDif="false"
    Zoom="75"
    Theme="Office2022">
</cc1:StiWebViewerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{ 
    StiWebViewerFx1.ShowPrintButton = false;
    StiWebViewerFx1.ShowSendEmailButton = true;
    StiWebViewerFx1.ShowTooltips = false;
    StiWebViewerFx1.ShowExportToDbf = false;
    StiWebViewerFx1.ShowExportToDif = false;
    StiWebViewerFx1.Zoom = 75;
    StiWebViewerFx1.Theme = StiViewerFxTheme.Office2022;
}
...
```

### Basic settings

| **Name** | **Description** |
| --- | --- |
| Width | Sets the width of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. The default width is 100%. |
| Height | Sets the height of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. The default height in 650 pixels. |


### Work with server

| **Name** | **Description** |
| --- | --- |
| RequestTimeout | Sets the response timeout from the server in seconds, after which an error will be generated. The default value is 20 seconds. For large reports, it is recommended to increase this value. |
| CacheTimeout | Sets the time in minutes that the server will store the report since the last action of the viewer, which requires the report to be rendered again (applying parameters, interactivity). The default value is 20 minutes. |
| CacheMode | Sets the report caching mode. It can take one of the following values of the **StiServerCacheMode** enumeration: **None** – caching is disabled, the report will be reloaded each time using the **OnGetReport** event; **ObjectCache** – the cache is used as the storage, the report is stored as an object (set by default); **ObjectSession** – the session is used as the storage, the report is stored as an object; **StringCache** – the server cache is used as the storage, the report is serialized to a packed string; **StringSession** – the session is used as a storage, the report is serialized into a packed string. |
| CacheItemPriority | Sets the priority of the report stored in the server cache. This property affects the automatic clearing of the server memory in case of lack of memory. The lower the priority is, the greater is the chance of removing information from memory. |
| RepeatCount | Sets the number of times to retry the request to the server when an error occurs in the response. The default value is **1**. |
| EnableDataLogger | Sets the logging mode of all requests for the viewer and server responses to a special repository. When you enable the property, a new **Save Log File** item will be added to the save report menu. It allows you to save the actions of the viewer to a text file. By default, the property is set to **false**. |
| UseRelativeUrls | Sets the viewer mode in which relative URLs are used for requests to the server. By default, the property is set to **true**. |
| PassQueryParametersForResources | Enables transferring all request URL parameters when generating links to the resources of the viewer. If **false**, only the necessary parameters are used to request the resources of the viewer. This corresponds to the more correct work of the browser cache. By default, the property is set to **true**. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| Theme | Specifies the theme of the viewers layout. The list of available themes can be found in the **StiViewerFxTheme** enumeration. The default value is **Office2022**. |
| Localization | Specifies the path to [the XML localization file](Localization.md). The path can be absolute or relative. By default, the English localization is used, which is built into the viewer and does not require additional XML files. |
| AboutDialogTextLine1 | Specifies the text to be added in the **About** box. By default, the standard text of the dialog box is displayed. |
| AboutDialogTextLine2 | Specifies additional text to be added in the **About** box. By default, there is no additional text. |
| AboutDialogUrl | Specifies a URL to the website of the developer. By default, the URL to the [Stimulsoft](https://stimulsoft.com) website is displayed. |
| AboutDialogUrlText | Specifies the link text to the website of the developer. By default, the link is displayed as text. |
| ShowCancelButton | Enables displaying the Cancel button in the load data from the server window. By default, the property is set to **false**. |
| BackgroundColor | Sets the background color of the viewer. By default it is set to **White**. |
| FlashWMode | Specifies the mode of showing the Flash viewer on the HTML page. It can take one of the following **StiWMode** enumeration values: **Window** – standard mode with an opaque background, the viewer is always placed above all HTML page objects (the default value); **Opaque** – opaque background with the ability to display HTML elements of the page over the viewer; **Direct** - opaque background, it is allowed to use hardware acceleration; **Transparent** – transparent background, should be used, if, under the viewer, there is a heterogeneous background or HTML elements of the page that should be visible. |
| AutoHideScrollbars | Enables automatic hiding of report scrollbars, if they are not required. By default, the property is set to **false**. |
| CurrentPageBorderColor | Sets the border color of the selected (current) report page. By default, the property is set to **Gold** (or **Blue** for the Office2022 theme). |
| ParametersPanelColumnsCount | Sets the number of columns to display report parameters. By default, there are 2 columns. |
| ParametersPanelEditorWidth | Sets the width of editable fields in the parameters panel. The default width is 200 pixels. |
| ParametersPanelDateFormat | Sets the date and time format for variables of the appropriate type in the parameters panel. By default, the date and time format, set on the server, is used. |
| OpenLinksWindow | Sets the target window for opening the links contained in the report. By default, the property is set to **Blank** (new window). |
| OpenExportedReportWindow | Sets the target window for opening the export file from the viewer. By default, the property is set to **Blank** (new window). |
| DesignWindow | Sets the target window for opening the report designer. By default, the property is set to **Self** (current window). |
| ImagesQuality | Sets the quality of image conversion. Used to display some components, such as RichText, some types of charts and bar-codes. The default value is set to **Normal**. |
| ShowTooltips | Enables displaying tooltips for the viewer controls when the mouse hovers over. By default, the property is set to **true**. |
| ShowTooltipsHelp | Enables displaying links to online documentation in tooltips for the viewer controls. By default, the property is set to **true**. |
| ShowFormsHelp | Enables displaying a link to online documentation in the titles of the dialog forms of the viewer. By default, the property is set to **true**. |
| ShowFormsHints | Enables displaying tooltips when hovering over the interface elements in the dialog boxes of the viewer. By default, the property is set to **true**. |
| BrowserTitle | Specifies the title of the browser window on the page on which the viewer is located. By default, the property has an empty value and the browser window title in this case remains unchanged. |


### Toolbar

| **Name** | **Description** |
| --- | --- |
| ShowToolbar | Enables showing the viewer toolbar. By default, the property is set to **true**. |
| ShowNavigatePanel | Enables the navigation panel for the report. By default, the property is set to **true**. |
| ShowViewModePanel | Enables showing the report preview panel. By default, the property is set to **true**. |
| ShowPrintButton | Enables showing the button - **Print** - on the toolbar of the viewer. By default, the property is set to **true**. |
| ShowOpenButton | Enables showing the button - **Open** - on the toolbar of the viewer. By default, the property is set to **false**. |
| ShowSaveButton | Enables showing the button - **Save** - on the toolbar of the viewer. By default, the property is set to **true**. |
| ShowSendEmailButton | Enables showing the button - **Send Email** - on the toolbar of the viewer. By default, the property is set to **false**. |
| ShowBookmarksButton | Enables showing the button - **Bookmarks** - on the toolbar of the viewer. By default, the property is set to **true**. If the button is hidden, the bookmarks panel will not be displayed even if there are bookmarks in the report. |
| ShowParametersButton | Enables showing the button - **Parameters** - on the toolbar of the viewer. By default, the property is set to **true**. If the button is hidden, the parameters panel will not be displayed even if there are parameters in the report. |
| ShowResourcesButton | Enables showing the button - **Resources** - on the toolbar of the viewer. By default, the property is set to **true**. If the button is hidden, the resources panel will not be displayed even if there are resources in the report. |
| ShowThumbnailsButton | Enables showing report page thumbnails in the special panel of the viewer. By default, the property is set to **true**. |
| ShowFindButton | Enables showing the button - **Find** - on the toolbar of the viewer. By default, the property is set to **true**. |
| ShowFullScreenButton | Enables showing the button - **Full Screen** - on the toolbar of the viewer. By default, the property is set to **true**. |
| ShowExitButton | Enables showing the button - **Exit** - on the toolbar of the viewer. By default, the property is set to **false**. |
| ShowAboutButton | Enables showing the button - **About** - on the toolbar of the viewer. By default, the property is set to **true**. |
| ShowDesignButton | Enables showing the button - **Design** - on the toolbar of the viewer. By default, the property is set to **false**. |
| ShowFirstPageButton | Enables showing the button - **First Page** -on the navigation panel of the viewer. By default, the property is set to **true**. |
| ShowPreviousPageButton | Enables showing the button - **Previous Page** - on the navigation panel of the viewer. By default, the property is set to **true**. |
| ShowGoToPageButton | Enables showing the button - **Go To Page** - on the navigation panel of the viewer. By default, the property is set to **true**. |
| ShowNextPageButton | Enables showing the button - **Next Page** - on the navigation panel of the viewer. By default, the property is set to **true**. |
| ShowLastPageButton | Enables showing the button - **Last Page** - on the navigation panel of the viewer. By default, the property is set to **true**. |
| ShowSinglePageViewModeButton | Enables showing the button - **Single Page** - on the report preview panel. By default, the property is set to **true**. |
| ShowContinuousPageViewModeButton | Enables showing the button - **Continuous Page** - on the report preview panel. By default, the property is set to **true**. |
| ShowMultiplePageViewModeButton | Enables showing the button - **Multiple Page** - on the report preview panel. By default, the property is set to **true**. |
| ShowZoomButtons | Enables showing zoom buttons. By default, the property is set to **true**. |
| Zoom | Sets the zoom for displaying report pages. The default setting is 100 percent. The values are from 10 to 500 percent. You can also set one of the following values: **StiZoomModeFx.OnePage** – when the viewer runs, the zoom to display the one report page will be set; **StiZoomModeFx.TwoPages** – when the viewer runs, the zoom to display two report pages will be set; **StiZoomModeFx.PageWidth** – when the viewer runs, the zoom to display the report by the width of the page will be set. |
| ExitUrl | Specifies the URL address for the **Exit** button of the report viewer. If the **OnExit** event handler is set, the value of this property will be ignored. By default, you will be redirected to the previous page corresponding to the browser history. |


### Export report

| **Name** | **Description** |
| --- | --- |
| ShowExportDialog | Enables showing export options dialog box. If the property is **false**, the export will be done with the default settings. By default the property is set to **true**. |
| ShowExportToDocument | Enables the export menu item **Document File**. By default, the property is set to **true**. |
| ShowExportToPdf | Enables the export menu item **Adobe PDF File**. By default, the property is set to **true**. |
| ShowExportToXps | Enables the export menu item **Microsoft XPS File**. By default, the property is set to **true**. |
| ShowExportToPowerPoint | Enables the export menu item **Microsoft PowerPoint 2007/2010 File**. By default, the property is set to **true**. |
| ShowExportToHtml | Enables the export menu item **HTML File**. By default, the property is set to **true**. |
| ShowExportToHtml5 | Enables the export menu item **HTML5 File**. By default, the property is set to **true**. |
| ShowExportToMht | Enables the export menu item **MHT Web Archive**. By default, the property is set to **true**. |
| ShowExportToText | Enables the export menu item **Text File**. By default, the property is set to **true**. |
| ShowExportToRtf | Enables the export menu item **Rich Text File**. By default, the property is set to **true**. |
| ShowExportToWord2007 | Enables the export menu item **Microsoft Word 2007/2010 File**. By default, the property is set to **true**. |
| ShowExportToOpenDocumentWriter | Enables the export menu item **OpenDocument Writer File**. By default, the property is set to **true**. |
| ShowExportToExcel | Enables the export menu item **Microsoft Excel File**. By default, the property is set to **true**. |
| ShowExportToExcelXml | Enables the export menu item **Microsoft Excel Xml File**. By default, the property is set to **true**. |
| ShowExportToExcel2007 | Enables the export menu item **Microsoft Word 2007/2010 File**. By default, the property is set to **true**. |
| ShowExportToOpenDocumentCalc | Enables the export menu item **OpenDocument Calc File**. By default, the property is set to **true**. |
| ShowExportToCsv | Enables the export menu item **CSV File**. By default, the property is set to **true**. |
| ShowExportToDbf | Enables the export menu item **DBF File**. By default, the property is set to **true**. |
| ShowExportToXml | Enables the export menu item **XML File**. By default, the property is set to **true**. |
| ShowExportToDif | Enables the export menu item **Data Interchange Format (DIF) File**. By default, the property is set to **true**. |
| ShowExportToSylk | Enables the export menu item **Symbolic Link (SYLK) File**. By default, the property is set to **true**. |
| ShowExportToImageBmp | Enables the export menu item **BMP Image**. By default, the property is set to **true**. |
| ShowExportToImageGif | Enables the export menu item **GIF Image**. By default, the property is set to **true**. |
| ShowExportToImageJpeg | Enables the export menu item **JPEG Image**. By default, the property is set to **true**. |
| ShowExportToImagePcx | Enables the export menu item **PCX Image**. By default, the property is set to **true**. |
| ShowExportToImagePng | Enables the export menu item **PNG Image**. By default, the property is set to **true**. |
| ShowExportToImageTiff | Enables the export menu item **TIFF Image**. By default, the property is set to **true**. |
| ShowExportToImageMetafile | Enables the export menu item **Windows Metafile**. By default, the property is set to **true**. |
| ShowExportToImageSvg | Enables the export menu item **Scalable Vector Graphics (SVG) File**. By default, the property is set to **true**. |
| ShowExportToImageSvgz | Enables the export menu item **Compressed SVG (SVGZ) File**. By default, the property is set to **true**. |


### Email

| **Name** | **Description** |
| --- | --- |
| ShowEmailDialog | Enables displaying settings for sending the report via email. If the dialog box is disabled, the email will be sent with the settings set on the server-side in the **OnEmailReport** event. By default the property is set to **true**. |
| ShowEmailExportDialog | Enables displaying export options dialog box when sending email. If the property is set to **false**, the export will be done with the default settings. By default the property is set to **true**. |
| DefaultEmailAddress | Sets the default recipient email, i.e. the address to which the email with the attached report will be sent. |


### Printing reports

| **Name** | **Description** |
| --- | --- |
| ShowPrintDialog | Enables displaying the report printing dialog box. If the print dialog is disabled, then, clicking the button, will immediately display the system print dialog, the report will be printed in the **Default** mode. By default, the property is set to **true**. |
| AutoPageOrientation | Enables automatic page rotation of the report if the report page orientation does not match the page orientation settings of the printer. By default, the property is set to **true**. |
| AutoPageScale | Enables automatic scaling of the report page to fit the paper size. By default, the property is set to **true**. |
| AllowDefaultPrint | Enables the **Default** report printing mode in the print report dialog box of the report viewer. By default, the property is set to **true**. |
| AllowPrintToPdf | Enables the **Print as PDF** report printing mode in the print report dialog box of the report viewer. By default, the property is set to **true**. |
| AllowPrintToHtml | Enables the **Print as HTML** report printing mode in the print report dialog box of the report viewer. By default, the property is set to **true**. |
| PrintAsBitmap | Enables report printing by means of a graphical snapshot of the report page. By default, the property is set to **true**. |
