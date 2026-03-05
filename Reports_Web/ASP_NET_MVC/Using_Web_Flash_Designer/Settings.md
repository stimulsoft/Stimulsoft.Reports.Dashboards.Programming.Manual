# Designer Settings

The **Flash Designer** configuration is done using properties that are located in the **StiMvcDesignerFxOptions** class. All properties are divided into groups, some of the groups contain subgroups of properties for ease of use. Below is an example of setting some properties of the designer.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesignerFx("MvcDesignerFx1", 
    new StiMvcDesignerFxOptions() {
        Theme = StiDesignerFxTheme.Office2022,
        Localization = "~/Content/Localization/en.xml",
        LocalizationDirectory = "~/Content/Localization",
        Actions =
        {
            GetReport = "GetReport",
            PreviewReport = "PreviewReport",
            SaveReport = "SaveReport",
            ExportReport = "ExportReport"
        },
        Behavior =
        {
            AutoSaveInterval = 3
        },
        PreviewToolbar =
        {
            ShowSendEmailButton = true
        },
        Print =
        {
            AutoPageOrientation = true,
            AutoPageScale = true   
        }
})
...
```

### Basic settings (without groups)

| **Name** | **Description** |
| --- | --- |
| Theme | Specifies the theme of the report designer. The list of available themes is located in the **StiDesignerFxTheme** enumeration. The default value is **Office2022**. |
| Localization | Specifies the path to [the XML localization file](Localization.md). The path can be absolute or relative. By default, English localization is used. It is built into the designer and does not require additional XML files. |
| LocalizationDirectory | Specifies the path to the directory with [XML localization files](Localization.md). The localization files located in the specified folder will be loaded to the localization list in the designer panel. |
| Width | Sets the width of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. The default width is 100%. |
| Height | Sets the height of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. The default height is 800 pixels. |


### Actions

| **Name** | **Description** |
| --- | --- |
| GetReport | Specifies the name of the action method to prepare [the report template when loading the designer](Editting_Report.md). |
| CreateReport | Specifies the name of the action method to prepare the report template when [creating the new report](Creating_Report.md) in the designer. |
| SaveReport | Specifies the name of the action method [to save the report template](Saving_Report.md) on the server-side. |
| SaveReportAs | Specifies the name of the action method to store the report template on the server-side when using the **Save As** menu item. If no action is specified, the built-in method of saving [the report template](Saving_Report.md) to the local disk will be used. |
| PreviewReport | Specifies the name of the action method to prepare the rendered report [in the preview window](Preview.md). |
| ExportReport | Specifies the name of the action method [to export reports](Additional_Functionality_of_Preview.md) to the specified format. |
| EmailReport | Specifies the name of the action method [to send the report by email](Additional_Functionality_of_Preview.md). |
| GetLocalization | Specifies the name of the action method to load the [XML localization file](Localization.md). If the action is not defined, English localization will be set. |
| Exit | Specifies the name of the action method to go to the desired view by clicking [the Exit button](Additional_Features_of_Designer.md) in the main menu of the report designer. |
| DesignerEvent | Specifies the name of the action method of the report designer to handle [additional designer actions](Additional_Features_of_Designer.md) such as working with data, previewing the report, viewing the C#/VB.Net report code, and others. Also, this action is used to load scripts and designer styles. |


### Server

| **Name** | **Description** |
| --- | --- |
| Controller | Specifies the name of the controller to process requests. If this property is not set, the current controller will be used to process the requests. |
| RouteTemplate | Sets the route template that is returned when the report designer actions are executed. If the property is not set, then the MVC project template will be used instead. The default value of the property is null. |
| RequestTimeout | Sets the response timeout from the server in seconds after which an error will be generated. The default value is set to 20 seconds. For big reports, it is recommended to increase this value. |
| CacheTimeout | Sets the time in minutes that the server will store the rendered report since the last action of the viewer. The default setting is 20 minutes. |
| CacheMode | Sets the report caching mode. It can take one of the following values of the **StiServerCacheMode** enumeration: **None** – caching is disabled. When printing and exporting, the report will be sent to every time to the server-side; **ObjectCache** – the cache is used as the storage, the report is stored as an object (set by default); **ObjectSession** – the session is used as the storage, the report is stored as an object; **StringCache** – the server cache is used as the storage, the report is serialized to a packed string; **StringSession** – the session is used as a repository, the report is serialized into a packed string. |
| CacheItemPriority | Sets the priority of the report stored in the server cache. This property affects the automatic clearing of the server memory in case of lack of memory. The lower the priority is, the greater is the chance of removing information from memory. |
| RepeatCount | Sets the number of times to retry the request to the server when an error occurs in the response. By default, the property is set to **1**. |
| EnableDataLogger | Sets the logging mode for all client-side requests and server responses to a special repository. When you enable the property, the new **Save Log File** item will be added to the menu. It allows you to save the query and response logs to a text file. By default, the property is set to **false**. |
| UseRelativeUrls | Sets the designer mode in which relative URLs are used for requests to the server. By default, the property is set to **true**. |
| PassQueryParametersForResources | Enables transferring all request URL parameters when generating links to the resources of the designer. If **false**, only the necessary parameters are used to request the resources of the designer. This corresponds to the more correct operation of the browser cache. By default, the property is set to **true**. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| AboutDialogTextLine1 | Specifies the text to be added in the **About** box. By default, the standard text of the dialog box is displayed. |
| AboutDialogTextLine2 | Specifies additional text to be added in the **About** box. There is no additional text by default. |
| AboutDialogUrl | Specifies a URL to the website of the developer. By default, the URL to the [Stimulsoft](https://stimulsoft.com) website is displayed. |
| AboutDialogUrlText | Specifies the URL text to the website of the developer. By default, the link is displayed as text. |
| ShowCancelButton | Enables displaying the Cancel button in the load data from the server window. By default, the property is set to **false**. |
| ShowMoreDetailsButton | Enables displaying the More Details button in the error message. By default, the property is set to **true**. |
| FlashWMode | Specifies the mode of showing the Flash designer on the HTML page. It can take one of the following **StiWMode** enumeration values: **Window** – standard mode with an opaque background, the designer is always placed above all HTML page objects (the default value); **Opaque** – opaque background with the ability to display HTML elements of the page over the designer; **Direct** - opaque background, it is allowed to use hardware acceleration; **Transparent** – transparent background, should be used, if, under the designer, there is a heterogeneous background or HTML elements of the page that should be visible. |
| ShowTooltips | Enables displaying tooltips for the designer controls when the mouse hovers over. By default, the property is set to **true**. |
| ShowTooltipsHelp | Enables displaying links to online documentation in tooltips for the designer controls. By default, the property is set to **true**. |
| ShowDialogsHelp | Enables displaying a link to online documentation in the titles of the dialog forms of the designer. By default, the property is set to **true**. |
| ShowDialogsHints | Enables displaying tooltips when hovering over the interface elements in the dialog boxes of the designer. By default, the property is set to **true**. |
| GridSizeInCentimetres | Specifies the grid size of the edit report page in centimeters. The default value is set to 0.2 centimeters. |
| GridSizeInHundredthsOfInches | Specifies the grid size of the edit report page in hundredths of inch. The default value is set to 10 hundredths of an inch. |
| GridSizeInInches | Specifies the grid size of the edit report page in inches. The default value is set to 0.1 inches. |
| GridSizeInMillimeters | Specifies the grid size of the edit report page in millimeters. The default value is set to 2 millimeters. |
| DateFormat | Specifies the date and time format for the dialog boxes of the designer, as well as for the variables of the corresponding type in the options panel. It can take a string mask of date and time on the input, as well as one of the following values: **StiDateFormatMode.FromClient** - the format of the date and time set on the client-side; **StiDateFormatMode.FromServer** - the date and time format set on the server-side (default value). |
| BrowserTitle | Specifies the title of the web browser window on the page on what the designer is placed. By default, the property has an empty value and the browser window title, in this case, remains unchanged. |
| AutoHideScrollbars | Enables automatic hiding of report scrollbars in the preview window. By default, the property is set to **false**. |
| CurrentPageBorderColor | Sets the border color of the selected (current) report page in the preview window. By default, the property is **Gold**, or **Blue** value for the **Office2022** theme. |
| ParametersPanelColumnsCount | Sets the number of columns to display report parameters in preview. By default, there are 2 columns. |
| ParametersPanelEditorWidth | Specifies the width of the editable fields in the report settings panel in the preview window. The default width is 200 pixels. |
| OpenLinksWindow | Specifies the target window for opening the links contained in the report. By default, the property is set to **Blank** (new window). |
| OpenExportedReportWindow | Specifies the target window for opening the exported file from the report preview window. By default, the property is set to **Blank** (new window). |
| ImagesQuality | Sets the quality of image conversion. Used to display some components, such as Rich Text, some types of charts and bar-codes. By default, the property is set to **Normal**. |


### Behavior

| **Name** | **Description** |
| --- | --- |
| ShowSaveDialog | Enables displaying the dialog to insert a report name when it is saved. The name of the report will be transferred in the parameters of the report designer. By default, the property is set to **false**. |
| SetReportModifiedWhenOpening | Specifies the report, opened when the designer runs, as already changed. By default, the property is set to **false**. |
| AutoSaveInterval | Specifies the time interval (in minutes) through which the designer automatically calls the action to save the report. The default value is set to 0 minutes (auto-saving is disabled). |
| SaveReportMode | Sets the mode to save reports. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (the default value); **Visible** - saving of the report will be called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report will be called in a new window (tab) of the web browser. |
| SaveReportAsMode | Sets the mode for saving the report. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (the default value); **Visible** - saving of the report is called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report is called in a new window (tab) of the web browser. |
| RunWizardAfterLoad | Enables displaying the window of the render report wizard when the designer runs. By default, the property is set to **false**. |
| DesignerEventFunction | Specifies the name of the JavaScript function that will be called when certain actions are taken by the designer. The function takes a string parameter to the input. The designer action ID is passed in it. |
| ExitUrl | Specifies the URL address when clicking the **Exit** button in the main menu of the designer. |


### Main Menu

| Name | Description |
| --- | --- |
| ShowNew | Enables showing the main menu item - **New**. By default, the property is set to **true**. |
| ShowNewReport | Enables showing the main menu item - **New Report**. By default, the property is set to **true**. |
| ShowNewReportWithWizard | Enables showing the main menu item - **New Report With Wizard**. By default, the property is set to **true**. |
| ShowNewPage | Enables showing the main menu item - **New Page**. By default, the property is set to **true**. |
| ShowOpenReport | Enables showing the main menu item - **Open Report**. By default, the property is set to **true**. |
| ShowSaveReport | Enables showing the main menu item - **Save Report**. By default, the property is set to **true**. |
| ShowSaveAs | Enables showing the main menu item - **Save Report As**. By default, the property is set to **true**. |
| ShowPreview | Enables showing the main menu item - **Preview**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowPreviewAsPdf | Enables showing the main menu item - **Preview as PDF**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowPreviewAsHtml | Enables showing the main menu item - **Preview as HTML**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowPreviewAsXps | Enables showing the main menu item - **Preview as XPS**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowClose | Enables showing the main menu item - **Close**. By default, the property is set to **true**. |
| ShowAbout | Enables showing the main menu item - **About**. By default, the property is set to **true**. |
| ShowExit | Enables showing the main menu item - **Exit**. By default, the property is set to **false**. |
| Caption | Specifies the title of the main menu of the report designer. By default, the standard title text is used. |


### Dictionary

| **Name** | **Description** |
| --- | --- |
| AllowModifyDictionary | Allows editing data dictionary. By default, the property is set to **true**. |
| AllowModifyConnections | Allows editing connections in the data dictionary. By default, the property is set to **true**. |
| AllowModifyDataSources | Allows editing data sources in the data dictionary. By default, the property is set to **true**. |
| AllowModifyRelations | Allows editing relations in the data dictionary. By default, the property is set to **true**. |
| AllowModifyVariables | Allows editing variables in the data dictionary. By default, the property is set to **true**. |
| ShowConnectionType | Enables showing a type of connection in the data dictionary. By default, the property is set to **true**. |
| ShowActionsMenu | Enables showing the menu - **Actions** - in the data dictionary. By default, the property is set to **true**. |
| ShowTestConnectionButton | Enables showing the button - **Test** - in the dialog box of editing the connection. By default, the property is set to **true**. |
| ShowOnlyAliasForBusinessObjects | Enables showing aliases for business objects. By default, the property is set to **false**. |
| ShowOnlyAliasForConnections | Enables showing aliases for connections. By default, the property is set to **false**. |
| ShowOnlyAliasForDataSources | Enables showing aliases for data sources. By default, the property is set to **false**. |
| ShowOnlyAliasForDataRelations | Enables showing aliases for relations. By default, the property is set to **false**. |
| ShowOnlyAliasForDataColumns | Enables showing aliases for data columns. By default, the property is set to **false**. |
| ShowOnlyAliasForVariables | Enables showing aliases for variables. By default, the property is set to **false**. |


### MainMenu

| **Name** | **Description** |
| --- | --- |
| ShowNew | Enables showing the main menu item - **New**. By default, the property is set to **true**. |
| ShowNewReport | Enables showing the main menu item - **New Report**. By default, the property is set to **true**. |
| ShowNewReportWithWizard | Enables showing the main menu item - **New Report With Wizard**. By default, the property is set to **true**. |
| ShowNewPage | Enables showing the main menu item - **New Page**. By default, the property is set to **true**. |
| ShowOpenReport | Enables showing the main menu item - **Open Report**. By default, the property is set to **true**. |
| ShowSaveReport | Enables showing the main menu item - **Save Report**. By default, the property is set to **true**. |
| ShowSaveAs | Enables showing the main menu item - **Save Report As**. By default, the property is set to **true**. |
| ShowPreview | Enables showing the main menu item - **Preview**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowPreviewAsPdf | Enables showing the main menu item - **Preview as PDF**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowPreviewAsHtml | Enables showing the main menu item - **Preview as HTML**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowPreviewAsXps | Enables showing the main menu item - **Preview as XPS**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowClose | Enables showing the main menu item - **Close**. By default, the property is set to **true**. |
| ShowAbout | Enables showing the main menu item - **About**. By default, the property is set to **true**. |
| ShowExit | Enables showing the main menu item - **Exit**. By default, the property is set to **false**. |
| Caption | Specifies the title of the main menu of the report designer. By default, the standard title text is used. |


### Toolbar

| **Name** | **Description** |
| --- | --- |
| ShowSelectLanguage | Enables a list of available localizations. By default, the property is set to **true**. |
| ShowCodeTab | Enables showing the preview window of the C#/VB.Net code of the edited report. By default, the property is set to **false**. |
| ShowPreviewReportTab | Enables showing the preview window of the report. By default, the property is set to **true**. |
| ShowDictionaryTab | Enables showing data dictionary. By default, the property is set to **true**. |
| ShowEventsTab | Enables showing report events tabs in the property editor panel. By default, the property is set to **true**. |
| Zoom | Specifies the zoom for displaying the report template edit page. The default zoom is set to 100 percent. The values vary from 10 to 500 percent. You can also set one of the following values: **StiZoomModeFx.Default** – when the designer runs, the previously used zoom value (the default value) will be set; **StiZoomModeFx.OnePage** – when the designer runs, the zoom, necessary to display the entire page in the designer window, will be set; **StiZoomModeFx.PageWidth** – when the designer runs, the zoom, necessary to display the report by the width of the page, will be set; **StiZoomModeFx.PageHeight** – when the designer runs, the zoom, necessary to display the report by the height, will be set. |


### PreviewToolbar

| **Name** | **Description** |
| --- | --- |
| Visible | Enables showing the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowNavigatePanel | Enables showing the report navigation panel in the preview window. By default, the property is set to **true**. |
| ShowViewModePanel | Enables showing the panel to select the report preview mode. By default, the property is set to **true**. |
| ShowPrintButton | Enables showing the button - **Print** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowOpenButton | Enables showing the button - **Open** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowSaveButton | Enables showing the button - **Save** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowSendEmailButton | Enables showing the button - **Send Email** - on the toolbar of the report preview window. By default, the property is set to **false**. |
| ShowBookmarksButton | Enables showing the button - **Bookmarks** - on the toolbar of the report preview window. By default, the property is set to **true**. If the specified button is hidden, the bookmarks bar will not be displayed even if there are bookmarks in the report. |
| ShowParametersButton | Enables showing the button - **Parameters** - on the toolbar of the report preview window. By default, the property is set to **true**. If the specified button is hidden, the parameters panel will not be displayed even if there are parameters in the report. |
| ShowThumbnailsButton | Enables showing thumbnails of report pages in the special panel of the report preview window. By default, the property is set to **true**. |
| ShowFindButton | Enables showing the button - **Find** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowFullScreenButton | Enables showing the button - **Full Screen** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowFirstPageButton | Enables showing the button - **First Page** - on the navigation panel of the report. By default, the property is set to **true**. |
| ShowPreviousPageButton | Enables showing the button - **Previous Page** - on the navigation panel of the report. By default, the property is set to **true**. |
| ShowGoToPageButton | Enables showing the button - **Go To Page** - on the navigation panel of the report. By default, the property is set to **true**. |
| ShowNextPageButton | Enables showing the button - **Next Page** - on the navigation panel of the report. By default, the property is set to **true**. |
| ShowLastPageButton | Enables showing the button - **Last Page** - on the navigation panel of the report. By default, the property is set to **true**. |
| ShowSinglePageViewModeButton | Enables showing the button - **Single Page** - on the panel to select the report preview mode. By default, the property is set to **true**. |
| ShowContinuousPageViewModeButton | Enables showing the button - **Continuous Page** - on the panel to select the report preview mode. By default, the property is set to **true**. |
| ShowMultiplePageViewModeButton | Enables showing the button - **Multiple Page** - on the panel to select the report preview mode. By default, the property is set to **true**. |
| ShowZoomButtons | Enables showing the buttons to select zoom in the preview window. By default, the property is set to **true**. |


### Behavior

| **Name** | **Description** |
| --- | --- |
| ShowSaveFileDialog | Enables displaying the dialog to insert a report name when it is saved. The name of the report will be transferred in the parameters of the report designer. By default, the property is set to **false**. |
| SetReportModifiedWhenOpening | Specifies the report, opened when the designer runs, as already changed. By default, the property is set to **false**. |
| AllowModifyTemplate | Allows editing the loaded report template elements. Creation and editing new items will be allowed regardless of the value of the property set. By default, the property is set to **true**. |
| AutoSaveInterval | Specifies the time interval (in minutes) through which the designer automatically calls the action to save the report. The default value is set to 0 minutes (auto-saving is disabled). |
| SaveReportMode | Sets the mode to save reports. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (the default value); **Visible** - saving of the report will be called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report will be called in a new window (tab) of the web browser. |
| SaveReportAsMode | Sets the mode for saving the report. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (the default value); **Visible** - saving of the report is called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report is called in a new window (tab) of the web browser. |
| RunWizardAfterLoad | Enables displaying the window of the render report wizard when the designer runs. By default, the property is set to **false**. |
| DesignerEventFunction | Specifies the name of the JavaScript function that will be called when certain actions are taken by the designer. The function takes a string parameter to the input. The designer action ID is passed in it. |
| ExitUrl | Specifies the URL address when clicking the **Exit** button in the main menu of the designer. |


### Export

| **Name** | **Description** |
| --- | --- |
| ShowExportDialog | Enables showing export options dialog box. If the property is **false**, the export will be done with the default settings. By default, the property is set to **true**. |
| ShowExportToDocument | Enables the export menu item - **Document File**. By default, the property is set to **true**. |
| ShowExportToPdf | Enables the export menu item - **Adobe PDF File**. By default, the property is set to **true**. |
| ShowExportToXps | Enables the export menu item - **Microsoft XPS File**. By default, the property is set to **true**. |
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
| ShowExportToExcel2007 | Enables the export menu item - **Microsoft Word 2007/2010 File**. By default, the property is set to **true**. |
| ShowExportToOpenDocumentCalc | Enables the export menu item - **OpenDocument Calc File**. By default, the property is set to **true**. |
| ShowExportToCsv | Enables the export menu item - **CSV File**. By default, the property is set to **true**. |
| ShowExportToDbf | Enables the export menu item - **DBF File**. By default, the property is set to **true**. |
| ShowExportToXml | Enables the export menu item - **XML File**. By default, the property is set to **true**. |
| ShowExportToDif | Enables the export menu item - **Data Interchange Format (DIF) File**. By default, the property is set to **true**. |
| ShowExportToSylk | Enables the export menu item - **Symbolic Link (SYLK) File**. By default, the property is set to **true**. |
| ShowExportToImageBmp | Enables the export menu item - **BMP Image**. By default, the property is set to **true**. |
| ShowExportToImageGif | Enables the export menu item - **GIF Image**. By default, the property is set to **true**. |
| ShowExportToImageJpeg | Enables the export menu item - **JPEG Image**. By default, the property is set to **true**. |
| ShowExportToImagePcx | Enables the export menu item - **PCX Image**. By default, the property is set to **true**. |
| ShowExportToImagePng | Enables the export menu item - **PNG Image**. By default, the property is set to **true**. |
| ShowExportToImageTiff | Enables the export menu item - **TIFF Image**. By default, the property is set to **true**. |
| ShowExportToImageMetafile | Enables the export menu item - **Windows Metafile**. By default, the property is set to **true**. |
| ShowExportToImageSvg | Enables the export menu item - **Scalable Vector Graphics (SVG) File**. By default, the property is set to **true**. |
| ShowExportToImageSvgz | Enables the export menu item - **Compressed SVG (SVGZ) File**. By default, the property is set to **true**. |


### Send report by email

| **Name** | **Description** |
| --- | --- |
| ShowEmailDialog | Enables displaying settings for sending the report via email. If the dialog box is disabled, the email will be sent with the settings set on the server-side in the **EmailReport** action. By default the property is set to **true**. |
| ShowExportDialog | Enables displaying export options dialog box when sending email. If the property is set to **false**, the export will be done with the default settings. By default the property is set to **true**. |
| DefaultEmailAddress | Sets the default recipient email, i.e. the address to which the email with the attached report will be sent. |


### Printing options

| **Name** | **Description** |
| --- | --- |
| ShowPrintDialog | Enables displaying the report printing dialog box. If the print dialog is disabled, then, clicking the button, will immediately display the system print dialog, the report will be printed in the **Default** mode. By default, the property is set to **true**. |
| AutoPageOrientation | Enables automatic page rotation of the report if the report page orientation does not match the page orientation settings of the printer. By default, the property is set to **true**. |
| AutoPageScale | Enables automatic scaling of the report page to fit the paper size. By default, the property is set to **true**. |
| AllowDefaultPrint | Enables the **Default** report printing mode in the print report dialog box of the report preview. By default, the property is set to **true**. |
| AllowPrintToPdf | Enables the **Print as PDF** report printing mode in the print report dialog box of the report preview. By default, the property is set to **true**. |
| AllowPrintToHtml | Enables the **Print as HTML** report printing mode in the print report dialog box of the report preview. By default, the property is set to **true**. |
| PrintAsBitmap | Enables report printing by means of a graphical snapshot of the report page. By default, the property is set to true. |
