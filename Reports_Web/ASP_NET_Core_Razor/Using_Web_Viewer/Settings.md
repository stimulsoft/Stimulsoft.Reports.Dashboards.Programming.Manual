# Viewer Settings

The **HTML5 Viewer** is configured using properties that are located in the **StiNetCoreViewerOptions** class. All properties are divided into groups. Some of the groups contain subgroups for ease of use. The following is an example of setting the properties of the viewer.


**Index.cshtml**

```
...
@Html.StiNetCoreViewer(new StiNetCoreViewerOptions() {
    Theme = StiViewerTheme.Office2022WhiteTeal,
    Localization = "Localization/en.xml",
    Actions =
    {
        GetReport = "GetReport",
        ViewerEvent = "ViewerEvent"
    },
    Appearance =
    {
        InterfaceType = StiInterfaceType.Auto,
        ScrollbarsMode = true,
        ShowTooltips = false
    },
    Exports =
    {
        DefaultSettings = 
        {
            ExportToPdf = 
            {
                CreatorString = "Company Name",
                ImageQuality = 0.75f
            }
        },
        ShowExportToDbf = false,
        ShowExportToDif = false   
    }
})
...
```

Please note that all dashboard elements have their own save options and full-screen buttons for preview. There are no special options to control displaying them, but they can be disabled through the properties of the element. The code below should be added after loading the report before passing it to the viewer.


**Index.cshtml.cs**

```csharp
...
var dbsElementInteraction = (report.GetComponentByName("RegionMap1") as Stimulsoft.Report.Dashboard.IStiElementInteraction).DashboardInteraction;
(dbsElementInteraction as Stimulsoft.Report.Dashboard.IStiInteractionLayout).ShowFullScreenButton = false;
(dbsElementInteraction as Stimulsoft.Report.Dashboard.IStiInteractionLayout).ShowSaveButton = false;
...
```

### Main settings (without groups)

| **Name** | **Description** |
| --- | --- |
| Theme | Sets the [viewer theme](Using_Themes.md). The list of available themes can be found in the **StiViewerTheme** enumeration. The default value is **Office2022WhiteBlue**. |
| Localization | Sets the path to the [XML localization file](Localization.md). The path can be absolute or relative. By default, the English localization is used. It is built into the viewer and does not require additional XML files. |
| Width | Sets the width of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. The default width is 100%. |
| Height | Sets the height of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. By default, the automatic height is set depending on the size of the report page, or 650 pixels in the view mode of the viewer with scrollbars. |


### Actions

| **Name** | **Description** |
| --- | --- |
| GetReport | Specifies the name of the action method for preparing [the rendered report](Showing_Reports.md). Specifies the name of the action method for preparing the constructed report. If report caching is enabled, this action will be called only once when the report is requested or if the requested report is not found in the server cache. |
| PrintReport | Specifies the name of the action method [of report printing](Printing_Reports.md). This is not relevant when viewing dashboards. |
| ExportReport | Specifies the name of the action method [of the export the report](Export.md) to the specified format. |
| EmailReport | Specifies the name of the action method [of sending the report by email](Send_Email.md). This is not relevant when viewing dashboards. |
| Interaction | Specifies the name of the action method for the viewer to work with interactive operations, such as using [parameters](Work_with_Parameters.md), [dynamic sorting, collapsing, and drill-down](Interaction.md). |
| DesignReport | Specifies the name of the action method to go to the specified view **by clicking** [the Design button](Call_Designer.md) on the viewer panel. |
| ViewerEvent | Specifies the name of the action method of basic [viewer events](Showing_Reports.md) and the processing actions of the viewer, such as printing and exporting a report, working with parameters, and interactivity, if these actions are not specified separately. In addition, this action is used to load scripts and styles of the viewer. This action is mandatory. |


### Server

| **Name** | **Description** |
| --- | --- |
| RouteTemplate | Sets the route template that is returned when the report viewer actions are executed. If the property is not set, then the Razor project template will be used instead. If the `UseRelativeUrls` property is set to `true`, the `BasePath` will not be respected for this property.The default value of this property is null. |
| AllowAutoUpdateCookies | Allows the viewer to update the cookies automatically on every request to the server. By default, cookies are set when creating the viewer, if they are not specified in the report. By default, the property is set to **false**. |
| AllowAntiforgeryToken | Allow the viewer to automatically request and send the antiforgery token. By default, the property is set to **true**. |
| RequestTimeout | Sets the response timeout from the server in seconds, after which an error will be generated. The default value is 20 seconds. For big reports, it is recommended to increase this value. |
| CacheTimeout | Sets the time in minutes that the server will store the report since the last action of the viewer. The default value is 20 minutes. |
| CacheMode | Sets the report caching mode. It can take one of the following values of the **StiServerCacheMode** enumeration: **None** – caching is disabled, the report will be reloaded each time using the **GetReport** event; **ObjectCache** – the cache is used as the storage, the report is stored as an object (default value); **ObjectSession** – the session is used as the storage, the report is stored as an object; **StringCache** – the server cache is used as the storage, the report is serialized to a packed string; **StringSession** – the session is used as storage, the report is serialized into a packed string. |
| CacheItemPriority | Sets the priority of the report stored in the server cache. This property affects the automatic clearing of the server memory in case of lack of memory. The lower the priority is, the greater is the chance of removing information from memory. |
| AllowAutoUpdateCache | Sets the mode for automatic cache update. The report stored in the cache or the server session will be automatically re-saved after a certain period of time when the viewer is idle (every 3 minutes). By default, the property is set to **true**. |
| UseRelativeUrls | Sets the viewer mode in which relative URLs are used for AJAX requests to the server. By default, the property is set to **true**. |
| PortNumber | Gets or sets a value that specifies the port number to use in the URL. A value of **0** defines automatic detection (default value). A value of **-1** removes the port number. |
| PassQueryParametersToReport | Enables using all the URL parameters of the request as the variable values. The variable names must match the parameters. The default value of the property is **false**. |
| PassQueryParametersForResources | Enables transferring all request URL parameters when generating links to the resources of the viewer. If **false**, only the necessary parameters are used to request the resources of the viewer. This corresponds to the correct work of the browser cache. By default, the property is set to **true**. |
| PassFormValues | Enables passing the values of the POST form to the client-side, if these values are required to be used in the actions of the viewer. If you enable this property, the additional **GetFormValues()** method will return a collection of form parameters. By default, the property is **false**. |
| ShowServerErrorPage | Enables displaying an HTML page with the details of the error that occurred on the server-side. When the property is enabled, the details of the error will be displayed in the viewer window. If the property is disabled, only the numeric error code and a short error text in the dialog box will be displayed. By default, the property is set to **true**. |
| UseCompression | Enables compression of the viewer requests into the GZip stream. Enables compression of the viewer requests into the GZip stream. That allows to decrease the amount of internet traffic but slows down the viewer slightly. The default value of the property is **false**. |
| UseCacheForResources | Enables caching of the component resources on the server-side. The following resources are supported - scripts, styles, and images. This option improves the load speed of the component and also reduces the server load in multi-client environments. The default value is **true**. |
| UseLocalizedCache | Sets a value that enables the use of a different cache depending on the selected localization. The default value of the property is **false**. |
| AllowLoadingCustomFontsToClientSide | Allows you to pass custom fonts to the client side and convert them to CSS style for the correct display of text as HTML with a specified font. By default, the property is set to **false**. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| CustomCss | Sets the path to the CSS file of the viewer's styles. The standard styles of the chosen theme will not be loaded if this property has got a value. The default value of the property is an empty string. |
| BackgroundColor | Sets the background color of the viewer. By default, it is set to **White**. |
| PageBorderColor | Sets the border color of the viewer. By default it is set to **Gray**. |
| RightToLeft | Sets the **Right to Left** mode for viewer controls. By default, the property is set to **false**. By default, the property is set to **false**. |
| FullScreenMode | Sets the full-screen display mode of the viewer. By default, the property is set to **false**. |
| ScrollbarsMode | Sets the preview mode with scrollbars. By default, the property is set to **false**. |
| OpenLinksWindow | Sets the target window for opening links contained in the report. By default, the property is set to **Blank** (new window). |
| OpenExportedReportWindow | Sets the target window for opening the export file from the viewer. By default, the property is set to **Blank** (new window). |
| DesignWindow | Sets the destination window for launching the report designer. The default value of the property is **Self** (which is the current window). |
| ShowTooltips | Enables showing tips for the viewer controls when the mouse hovers over. By default, the property is set to **true**. |
| ShowTooltipsHelp | Enables showing links to online documentation for the viewer controls. By default, the property is set to **true**. |
| ShowDialogsHelp | Sets a value that indicates that showing or hiding the help button in dialogs. By default, the property is set to **true**. |
| PageAlignment | Sets the position of the report page in the viewer window. It can take one of the following values of the **StiContentAlignment** enumeration: **Left** – the page will be aligned left; **Center** – the page will be centered (default value); **Right** – the page will be aligned right. |
| ShowPageShadow | Enables displaying shadow for report pages. By default, the property is set to **true**. |
| BookmarksPrint | Enables printing of report bookmarks (besides the report itself). By default, the property is set to **false**. |
| BookmarksTreeWidth | Sets the width of the bookmarks panel in pixels. By default, the width is 180 pixels. |
| ParametersPanelPosition | Specifies the position of the report parameters panel. It can take one of the following **StiParametersPanelPosition** enumeration values: **Top** - the panel will be docked to the top margin (default value); **Left** - the panel will be docked to the left margin. |
| ParametersPanelMaxHeight | Sets the maximum height of the parameters bar in pixels. By default, the maximum height is 300 pixels. |
| ParametersPanelColumnsCount | Sets the number of columns to display report parameters. By default, there are 2 columns. |
| ParametersPanelSortDataItems | Gets or sets a value which indicates that variable items will be sorted. By default, the property is set to **true**. |
| ParametersPanelDateFormat | Sets the date and time format for variables of the corresponding type in the parameters panel. By default, the date and time format set by the browser is used. |
| InterfaceType | Sets the type of interface used for the viewer. It can take one of the following **StiInterfaceType** enumeration values: **Auto** – the viewer's interface is determined automatically depending of the device that is report is displayed on. That is the default value. **Mouse** – the standard interface with a mouse control will be used for all the screen types. **Touch** – the Touch interface will be used to control the viewer. The interface design was optimized for the 'touchscreen' display types. The viewer interface elements have been increased in size to simplify the control of the viewer and to improve its usability. **Mobile** - the Mobile interface will be used to control the viewer for all the screen types. The Mobile interface was designed to control the viewer using the mobile smartphone display. This interface design was simplified and adapted to use with the smartphones. |
| AllowMobileMode | Enables or disables displaying a report or dashboard in the mobile mode. If the option is set to **false**, then the mobile view will not be used. If the option is set to **true**, the mobile view mode will be used when opening the viewer on mobile devices. By default, the option is set to **true**. |
| ChartRenderType | Sets the displaying mode of charts on the report page. It can take one of the following **StiChartRenderType** enumeration values: **Image** – charts are displayed as static images; **Vector** – charts are displayed in the vector mode as an SVG object; **AnimatedVector** - charts are displayed in the vector mode as an SVG object, the chart elements are displayed with animation (default value). |
| ReportDisplayMode | Sets the export mode for displaying report pages. It can take one of the following values of the **StiReportDisplayMode** enumeration: **FromReport** - the export mode of the report elements is defined from report template settings - Div or Table; **Table** – report elements are exported using HTML tables (default value); **Div** – report elements are exported using DIV markup; **Span** - report items are exported using SPAN markup. |
| DatePickerFirstDayOfWeek | Sets the first day of the week for the date picker. It can take one of the following values of the **StiFirstDayOfWeek** enumeration: **Auto** – automatic detection of the first day of the week from the browser settings (default value); **Monday** – the first day of the week is Monday; **Sunday** – the first day of the week is Sunday. |
| DatePickerIncludeCurrentDayForRanges | Sets a value, which indicates that the current day will be included in the ranges of the date picker. By default, the property is set to **false**. |
| AllowTouchZoom | Sets ability to change the scale of the report page by using the two-fingers gesture (Pinch to Zoom) for the touch-screens. The default value of the property is **true**. |
| ShowReportIsNotSpecifiedMessage | Sets a value which indicates that 'The report is not specified' message will be shown. The default value of the property is **true**. |
| PrintToPdfMode | Sets the Print to PDF mode. It has the following values: **StiPrintToPdfMode.Hidden** - hidden print mode (default value); **StiPrintToPdfMode.Popup** - the PDF document will be displayed before printing in a pop-up window. |
| ImagesQuality | Gets or sets the image quality that will be used on the viewer page. It has the following values: **StiImagesQuality.Low**  -  low quality, used to speed up loading reports and saves memory; **StiImagesQuality.Normal**  -  normal quality, suitable for most cases (default value); **StiImagesQuality.High**  -  high quality, used for ultra high-definition displays, but may slow down the loading of pages. |
| CombineReportPages | Sets a value which indicates that if a report contains several pages, then they will be combined in preview. By default, the property is set to **false**. |
| AllowPropagationEvents | Allows the propagation of key press events when the report viewer is not in focus. By default, the property is set to **true**. |
| DashboardFilterElementItemHeight | Sets the height in pixel of the checkbox in the List Box dashboard element. |


### Toolbar

| **Name** | **Description** |
| --- | --- |
| Visible | Enables displaying the viewer toolbar. By default, the property is set to **true**. |
| DisplayMode | Specifies the display mode of the toolbar of the viewer. It can take one of the following values of the **StiToolbarDisplayMode** enumeration: **Simple** - all controls are located on the same control panel (default value); **Separated** - the control panel is split into top and bottom panels. |
| BackgroundColor | Specifies the background color of the viewer toolbar. The default color of the selected theme is used. |
| BorderColor | Specifies the border color of the viewer toolbar. The default color of the selected theme is used. |
| FontColor | Specifies the text color for the toolbar and the viewer menu. The default color of the selected theme is used. |
| FontFamily | Specifies the font for the toolbar and the viewer menu. The default font of the selected theme is used. |
| Alignment | Sets the alignment mode for the controls on the viewer toolbar. It can take one of the following values of the **StiContentAlignment** enumeration: **Left** – elements will be aligned left; **Center** – elements will be centered; **Right** – elements will be aligned right; **Default** – the alignment depends on the RightToLeft property (default value). |
| ShowButtonCaptions | Enables text of the buttons on the toolbar of the viewer. By default, the property is set to **true**. |
| ShowPrintButton | Enables showing the button - **Print** - on the viewer toolbar. By default, the property is set to **true**. |
| ShowOpenButton | Enables displaying the **Open** button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to **true**. |
| ShowSaveButton | Enables displaying the **Save** button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to true. |
| ShowSendEmailButton | Enables showing the button - **Send Email** - on the viewer toolbar. By default, the property is set to **false**. Also, you should [add the EmailReport action](Send_Email.md). |
| ShowFindButton | Enables showing the button - **Find** - on the viewer toolbar. By default, the property is set to **true**. |
| ShowBookmarksButton | Enables showing the button - **Bookmarks** - on the viewer toolbar. By default, the property is set to **true**. If the button is hidden, the bookmarks panel will not be displayed even if there are bookmarks in the report. |
| ShowParametersButton | Enables showing the button - **Parameters** - on the viewer toolbar. By default, the property is set to **true**. If the button is hidden, the parameters panel will not be displayed even if there are parameters in the report. |
| ShowResourcesButton | Enables showing the button - **Resources** - on the toolbar of the viewer. By default, the property is set to **true**. If the button is hidden, the resources panel will not be displayed even if there are resources in the report. |
| ShowEditorButton | Enables showing the button - **Editor** - on the viewer toolbar. By default, the property is set to **true**. |
| ShowFullScreenButton | Enables displaying the **Full Screen** button on the toolbar of the viewer when viewing reports or dashboards. . By default, the property is set to **true**. |
| ShowFirstPageButton | Enables showing the button - **First Page** - on the viewer toolbar. By default, the property is set to **true**. |
| ShowPreviousPageButton | Enables showing the button - **Previous Page** - on the viewer toolbar. By default, the property is set to **true**. |
| ShowCurrentPageControl | Enables showing the current report page indicator. By default, the property is set to **true**. |
| ShowNextPageButton | Enables showing the button - **Next Page** - on the viewer toolbar. By default, the property is set to **true**. |
| ShowLastPageButton | Enables showing the button - **Last Page** - on the toolbar of the viewer. By default, the property is set to **true**. |
| ShowZoomButton | Enables showing the button to select the report zoom. By default, the property is set to **true**. |
| ShowViewModeButton | Enables showing the button to select the view mode of the report page. By default, the property is set to **true**. |
| ShowDesignButton | Enables displaying the **Design** button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to **false**. |
| ShowAboutButton | Enables showing the button - **About** - on the viewer toolbar. By default, the property is set to **true**. |
| ShowRefreshButton | Sets a visibility of the **Refresh** button in the toolbar of the viewer. By default, the property is set to **true**. |
| ShowPinToolbarButton | Enables displaying of the **Pin Toolbar** button on the viewer's toolbar. The button is available only in the Mobile mode of the viewer's interface. The default value of the property is **true**. |
| PrintDestination | Sets the report printing mode. It can take one of the following values of the **StiPrintDestination** enumeration: **Default** – a menu with a choice of printing modes will be displayed (default value); **Pdf** – printing will be done in the PDF format; **Direct** – printing will be done to the HTML format directly to the printer, the system print dialog will be displayed; **PopupWindow** – printing will be done in the HTML format via the preview window of the report. |
| ViewMode | Sets the mode for displaying report pages. It can take one of the following **StiWebViewMode** enumeration values: **SinglePage** - displays one page of the report selected in the toolbar of the viewer (default value); **Continuous** - displays all pages of the report; **MultiplePages** - displays all report pages as a table. |
| Zoom | Sets the zoom for displaying report pages. The default setting is 100 percent. The values are from 10 to 500 percent. You can also set one of the following values: **StiZoomMode.PageWidth** – when the viewer runs, the zoom, necessary to display the report by the page width, will be set; **StiZoomMode.PageHeight** – when the viewer runs, the zoom, necessary to display the report by the page height, will be set. |
| MenuAnimation | Enables animation when the viewer menu shows/hides. By default the property is set to **true**. |
| ShowMenuMode | Sets the display mode of the viewer menu. It can take one of the following values of the **StiShowMenuMode** enumeration: **Click** – shows menu by mouse click (default value); **Hover** – shows menu by hovering the mouse cursor. |
| AutoHide | Enables auto-hiding of the viewer's toolbar. The property will work only for the Mobile mode of the viewer's interface. The default value of the property is **false**. |


### Export

| **Name** | **Description** |
| --- | --- |
| DefaultSettings | This group of properties provides the ability to specify the default export settings for each export type. These settings will be applied to the export dialogs when the viewer runs or to the report, if export dialogs are disabled. |
| StoreExportSettings | Enables saving selected settings in the export dialogs. Settings will be stored in browser cookies. By default the property is set to **true**. |
| ShowExportDialog | Enables showing the export options dialog box. If the property is set to **false**, the export will be done with the default settings. By default the property is set to **true**. |
| ShowExportToDocument | Enables the export menu item - **Document File**. By default, the property is set to **true**. |
| ShowExportToPdf | Enables displaying the **Adobe PDF file** export menu item when viewing reports, and the **Adobe PDF** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToXps | Enables the export menu item - **Microsoft XPS File**. By default, the property is set to **false**. |
| ShowExportToPowerPoint | Enables the export menu item - **Microsoft PowerPoint 2007/2010 File**. By default, the property is set to **true**. |
| ShowExportToHtml | Enables the export menu item - **HTML File**. By default, the property is set to **true**. |
| ShowExportToHtml5 | Enables the export menu item - **HTML5 File**. By default, the property is set to **true**. |
| ShowExportToMht | Enables the export menu item - **MHT Web Archive**. By default, the property is set to **true**. |
| ShowExportToText | Enables the export menu item - **Text File**. By default, the property is set to **true**. |
| ShowExportToRtf | Enables the export menu item - **Rich Text File**. By default, the property is set to **true**. |
| ShowExportToWord2007 | Enables the export menu item - **Microsoft Word 2007/2010 File**. By default, the property is set to **true**. |
| ShowExportToOpenDocumentWriter | Enables the export menu item - **OpenDocument Writer File**. By default, the property is set to **true**. |
| ShowExportToExcel | Enables the export menu item - **Microsoft Excel File**. By default, the property is set to **true**. |
| ShowExportToExcelXml | Enables the export menu item - **Microsoft Excel Xml File**. By default, the property is set to **true**. |
| ShowExportToExcel2007 | Enables displaying the **Microsoft Excel 2007/2010 File** export menu item when viewing reports, and the **Microsoft Excel** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToOpenDocumentCalc | Enables the export menu item - **OpenDocument Calc File**. By default, the property is set to **true**. |
| ShowExportToCsv | Enables the export menu item - **CSV File**. By default, the property is set to **true**. |
| ShowExportToDbf | Enables the export menu item - **DBF File**. By default, the property is set to **true**. |
| ShowExportToXml | Enables the export menu item - **XML File**. By default, the property is set to **true**. |
| ShowExportToDif | Enables the export menu item - **Data Interchange Format (DIF) File**. By default, the property is set to **true**. |
| ShowExportToSylk | Enables the export menu item - **Symbolic Link (SYLK) File**. By default, the property is set to **true**. |
| ShowExportToJson | Enables the export menu item - **JSON** **File**. By default, the property is set to **true**. |
| ShowExportToImageBmp | Enables displaying the **BMP Image** export menu item when viewing reports, and the **BMP Image** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToImageGif | Enables displaying the **GIF** **Image** export menu item when viewing reports, and the **GIF** **Image** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToImageJpeg | Enables displaying the **JPEG Image** export menu item when viewing reports, and the **JPEG Image** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToImagePcx | Enables displaying the **PCX Image** export menu item when viewing reports, and the **PCX Image** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToImagePng | Enables displaying the **PNG Image** export menu item when viewing reports, and the **PNG Image** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToImageTiff | Enables displaying the **TIFF Image** export menu item when viewing reports, and the **TIFF Image** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToImageSvg | Enables displaying the **Scalable Vector Graphics (SVG) File** export menu item when viewing reports, and the **Scalable Vector Graphics (SVG) File** item when viewing dashboards. By default, the property is set to **true**. |
| ShowExportToImageSvgz | Enables displaying the **Compressed SVG (SVGZ) File** export menu item when viewing reports, and the **Compressed SVG (SVGZ) File** item when viewing dashboards. By default, the property is set to **true**. |
| ShowOpenAfterExport | Enables displaying the **Open After Export** parameter in export settings menu. By default, the property is set to **true**. |


### Email

| **Name** | **Description** |
| --- | --- |
| ShowEmailDialog | Enables displaying settings for sending the report via email. If the dialog box is disabled, the email will be sent with the settings set on the server side in the **EmailReport** action. By default the property is set to **true**. |
| ShowExportDialog | Enables displaying export options dialog box when sending email. If the property is set to **false**, the export will be done with the default settings. By default the property is set to **true**. |
| DefaultEmailAddress | Sets the default recipient email, i.e. the address to which the email with the attached report will be sent. |
| DefaultEmailSubject | Sets the default email subject (header). |
| DefaultEmailMessage | Sets the default email message (text). |
| DefaultEmailReplyTo | Gets or sets the default text of the replyTo of the message created in the viewer. |
