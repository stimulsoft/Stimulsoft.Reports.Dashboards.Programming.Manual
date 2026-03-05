# Designer Settings

The **Flash Designer** can be configured using the component properties that can be set on the ASPX page or using the C#/VB code. Below are examples of setting designer properties.


**Default.aspx**

```
...
<cc1:StiWebDesignerFx ID="StiWebDesignerFx1" runat="server"
    AllowModifyConnections="false"
    AllowModifyDataSources="false"
    MainMenuShowOpenReport="false"
    RequestTimeout="300"
    AutoSaveInterval="3"
    Localization="Localization/de.xml"
    Theme="Office2022">
</cc1:StiWebDesignerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{ 
    StiWebDesignerFx1.AllowModifyConnections = false;
    StiWebDesignerFx1.AllowModifyDataSources = false;
    StiWebDesignerFx1.MainMenuShowOpenReport = false;
    StiWebDesignerFx1.RequestTimeout = 75;
    StiWebDesignerFx1.AutoSaveInterval = 75;
    StiWebDesignerFx1.Localization = "Localization/de.xml";
    StiWebDesignerFx1.Theme = StiDesignerFxTheme.Office2022;
}
...
```

### Basic Settings

| **Name** | **Description** |
| --- | --- |
| Width | Sets the width of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. The default width is 100%. |
| Height | Sets the height of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. The default height is 800 pixels. |


### Server

| **Name** | **Description** |
| --- | --- |
| RequestTimeout | Sets the time to wait for a response from the server in seconds, after which an error will be generated. The default value is 20 seconds. For big reports, it is recommended to increase this value. |
| CacheTimeout | Sets the time in minutes that the server will store the rendered report since the last action of the viewer. The default setting is 20 minutes. |
| CacheMode | Sets the report caching mode. It can take one of the following values of the **StiServerCacheMode** enumeration: **None** – caching is disabled, the report will be reloaded each time using the **OnGetReport** event; **ObjectCache** – the cache is used as the storage, the report is stored as an object (set by default); **ObjectSession** – the session is used as the storage, the report is stored as an object; **StringCache** – the server cache is used as the storage, the report is serialized to a packed string; **StringSession** – the session is used as a repository, the report is serialized into a packed string. |
| CacheItemPriority | Sets the priority of the report stored in the server cache. This property affects the automatic clearing of the server memory in case of lack of memory. The lower the priority is, the greater is the chance of removing information from memory. |
| RepeatCount | Sets the number of times to retry the request to the server when an error occurs in the response. By default, the property is set to **1**. |
| EnableDataLogger | Sets the logging mode for all client-side requests and server responses to a special repository. When you enable the property, the new **Save Log File** item will be added to the menu. It allows you to save the query and response logs to a text file. By default, the property is set to **false**. |
| UseRelativeUrls | Sets the designer mode in which relative URLs are used for requests to the server. By default, the property is set to **true**. |
| PassQueryParametersForResources | Enables transferring all request URL parameters when generating links to the resources of the designer. If **false**, only the necessary parameters are used to request the resources of the designer. This corresponds to the more correct operation of the browser cache. By default, the property is set to **true**. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| Theme | Specifies the theme of the designer layout. The list of available themes can be found in the **StiDesignerFxTheme** enumeration. The default value is **Office2022**. |
| Localization | Specifies the path to the XML localization file. The path can be absolute or relative. By default, the English localization is used, which is built into the viewer and does not require additional XML files. |
| LocalizationDirectory | Specifies the path to the directory with XML [localization files](Localization.md). The localization files located in the specified folder will be loaded to the localization list in the designer panel. |
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
| DateFormat | Specifies the date and time format for the dialog boxes of the designer, as well as for the variables of the corresponding type in the options panel. It can take on the input a string mask of date and time, as well as one of the following values: **StiDateFormatMode.FromClient** - the format of the date and time set on the client-side will be used; **StiDateFormatMode.FromServer** - the date and time format set on the server-side (default value). |
| BrowserTitle | Specifies the title of the web browser window on the page on what the designer is placed. By default, the property has an empty value and the browser window title, in this case, remains unchanged. |
| AutoHideScrollbars | Enables automatic hiding of report scrollbars in the preview window. By default, the property is set to **false**. |
| CurrentPageBorderColor | Sets the border color of the selected (current) report page in the preview window. By default, the property is **Gold**, or **Blue** value for the **Office2022** theme. |
| ParametersPanelColumnsCount | Sets the number of columns to display report parameters in preview. By default, there are 2 columns. |
| ParametersPanelEditorWidth | Specifies the width of the editable fields in the report settings panel in the preview window. The default width is 200 pixels. |
| OpenLinksWindow | Specifies the target window for opening the links contained in the report. By default, the property is set to **Blank** (new window). |
| OpenExportedReportWindow | Specifies the target window for opening the exported file from the report preview window. By default, the property is set to **Blank** (new window). |
| ImagesQuality | Sets the quality of image conversion. Used to display some components, such as **Rich Text**, some types of charts and bar-codes. By default, the property is set to **Normal**. |


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
| ShowFileMenuNew | Enables showing the main menu item - **New**. By default, the property is set to **true**. |
| ShowFileMenuNewReport | Enables showing the main menu item - **New Report**. By default, the property is set to **true**. |
| ShowFileMenuNewReportWithWizard | Enables showing the main menu item - **New Report With Wizard**. By default, the property is set to **true**. |
| ShowFileMenuNewPage | Enables showing the main menu item - **New Page**. By default, the property is set to **true**. |
| ShowFileMenuOpen | Enables showing the main menu item - **Open Report**. By default, the property is set to **true**. |
| ShowFileMenuSave | Enables showing the main menu item - **Save Report**. By default, the property is set to **true**. |
| ShowFileMenuSaveAs | Enables showing the main menu item - **Save Report As**. By default, the property is set to **true**. |
| ShowFileMenuPreview | Enables showing the main menu item - **Preview**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowFileMenuPreviewAsPdf | Enables showing the main menu item - **Preview as PDF**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowFileMenuPreviewAsHtml | Enables showing the main menu item - **Preview as HTML**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowFileMenuPreviewAsXps | Enables showing the main menu item - **Preview as XPS**. Available only for the theme - **Office2007Blue**. By default, the property is set to **true**. |
| ShowFileMenuClose | Enables showing the main menu item - **Close**. By default, the property is set to **true**. |
| ShowFileMenuAbout | Enables showing the main menu item - **About**. By default, the property is set to **true**. |
| ShowFileMenuExit | Enables showing the main menu item - **Exit**. By default, the property is set to **true**. |
| FileMenuCaption | Specifies the title of the main menu of the report designer. By default, the standard title text is used. |


### Data dictionary

| **Name** | **Description** |
| --- | --- |
| AllowModifyDictionary | Allows editing data dictionary. By default, the property is set to **true**. |
| AllowModifyConnections | Allows editing connections in the data dictionary. By default, the property is set to **true**. |
| AllowModifyDataSources | Allows editing data sources in the data dictionary. By default, the property is set to **true**. |
| AllowModifyRelations | Allows editing connections in the data dictionary. By default, the property is set to **true**. |
| AllowModifyVariables | Allows editing variables in the data dictionary. By default, the property is set to **true**. |
| ShowConnectionType | Enables showing the type of connection in the data dictionary. By default, the property is set to **true**. |
| ShowActionsMenu | Enables showing the **Actions** menu in the data dictionary. By default, the property is set to **true**. |
| ShowTestConnectionButton | Enables showing the **Test** button in the edit connection dialog. By default, the property is set to **true**. |
| ShowOnlyAliasForBusinessObjects | Enables showing the mode of showing aliases for business objects. By default, the property is set to **false**. |
| ShowOnlyAliasForConnections | Enables showing the mode of showing aliases for connections. By default, the property is set to **false**. |
| ShowOnlyAliasForDataSources | Enables showing the mode of showing aliases for data sources. By default, the property is set to **false**. |
| ShowOnlyAliasForDataRelations | Enables showing the mode of showing aliases for relations. By default, the property is set to **false**. |
| ShowOnlyAliasForDataColumns | Enables showing the mode of showing aliases for columns. By default, the property is set to **false**. |
| ShowOnlyAliasForVariables | Enables showing the mode of showing aliases for variables. By default, the property is set to **false**. |


### Main menu

| **Name** | **Description** |
| --- | --- |
| ShowFileMenuNew | Enables showing the **New** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuNewReport | Enables showing the **New Report** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuNewReportWithWizard | Enables showing the **New Report With Wizard** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuNewPage | Enables showing the **New Page** item of the main menu. By default, the property is set to true. |
| ShowFileMenuOpen | Enables showing the **Open Report** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuSave | Enables showing the **Save Report** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuSaveAs | Enables showing the **Save Report As** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuPreview | Enables showing the **Preview** item of the main menu. Available only for the **Office2007Blue** theme. By default, the property is set to **true**. |
| ShowFileMenuPreviewAsPdf | Enables showing the **Preview as PDF** item of the main menu. Available only for the **Office2007Blue** theme. By default, the property is set to **true**. |
| ShowFileMenuPreviewAsHtml | Enables showing the **Preview as HTML** item of the main menu. Available only for the **Office2007Blue** theme. By default, the property is set to **true**. |
| ShowFileMenuPreviewAsXps | Enables showing the **Preview as XPS** item of the main menu. Available only for the **Office2007Blue** theme. By default, the property is set to **true**. |
| ShowFileMenuClose | Enables showing the **Close** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuAbout | Enables showing the **About** item of the main menu. By default, the property is set to **true**. |
| ShowFileMenuExit | Enables showing the **Exit** item of the main menu. By default, the property is set to **true**. |
| FileMenuCaption | Specifies the title of the main menu. By default, the standard title is used. |


### Toolbar

| **Name** | **Description** |
| --- | --- |
| ShowSelectLanguage | Enables a list of available localizations. By default, the property is set to **true**. |
| ShowCodeTab | Enables showing the preview window of the C#/VB.Net code of the edited report. By default, the property is set to **false**. |
| ShowPreviewReportTab | Enables showing the report preview window. By default, the property is set to **true**. |
| ShowDictionaryTab | Enables showing data dictionary. By default, the property is set to **true**. |
| ShowEventsTab | Enables showing report events tabs in the property editor panel. By default, the property is set to **true**. |
| Zoom | Specifies the zoom for displaying the report template edit page. The default zoom is set to 100 percent. The values vary from 10 to 500 percent. You can also set one of the following values: **StiZoomModeFx.Default** – when the designer runs, the previously used zoom value (the default value) will be set; **StiZoomModeFx.OnePage** – when the designer runs, the zoom, necessary to display the entire page in the designer window, will be set; **StiZoomModeFx.PageWidth** – when the designer runs, the zoom, necessary to display the report by the width of the page, will be set; **StiZoomModeFx.PageHeight** – when the designer runs, the zoom, necessary to display the report by the height, will be set. |


### Preview window toolbar

| **Name** | **Description** |
| --- | --- |
| ShowPreviewToolbar | Enables showing the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowPreviewNavigatePanel | Enables showing the report navigation panel in the preview window. By default, the property is set to **true**. |
| ShowPreviewViewModePanel | Enables showing the panel to select the report preview mode. By default, the property is set to **true**. |
| ShowPreviewPrintButton | Enables showing the button - **Print** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowPreviewOpenButton | Enables showing the button - **Open** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowPreviewSaveButton | Enables showing the button - **Save** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowPreviewSendEmailButton | Enables showing the button - **Send Email** - on the toolbar of the report preview window. By default, the property is set to **false**. |
| ShowPreviewBookmarksButton | Enables showing the button - **Bookmarks** - on the toolbar of the report preview window. By default, the property is set to **true**. If the specified button is hidden, the bookmarks bar will not be displayed even if there are bookmarks in the report. |
| ShowPreviewParametersButton | Enables showing the button - **Parameters** - on the toolbar of the report preview window. By default, the property is set to **true**. If the specified button is hidden, the parameters panel will not be displayed even if there are parameters in the report. |
| ShowPreviewThumbnailsButton | Enables showing thumbnails of report pages in the special panel of the report preview window. By default, the property is set to **true**. |
| ShowPreviewFindButton | Enables showing the button - **Find** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowPreviewFullScreenButton | Enables showing the button - **Full Screen** - on the toolbar of the report preview window. By default, the property is set to **true**. |
| ShowPreviewFirstPageButton | Enables showing the button - **First Page** - on the navigation panel. By default, the property is set to **true**. |
| ShowPreviewPreviousPageButton | Enables showing the button - **Previous Page** - on the navigation panel. By default, the property is set to **true**. |
| ShowPreviewGoToPageButton | Enables showing the button - **Go To Page** - on the navigation panel. By default, the property is set to **true**. |
| ShowPreviewNextPageButton | Enables showing the button - **Next Page** - on the navigation panel. By default, the property is set to **true**. |
| ShowPreviewLastPageButton | Enables showing the button - **Last Page** - on the navigation panel. By default, the property is set to **true**. |
| ShowPreviewSinglePageViewModeButton | Enables showing the button - **Single Page** - on the preview mode panel. By default, the property is set to **true**. |
| ShowPreviewContinuousPageViewModeButton | Enables showing the button - **Continuous Page** - on the preview mode panel. By default, the property is set to **true**. |
| ShowPreviewMultiplePageViewModeButton | Enables showing the button - **Multiple Page** - in the panel to select the report preview mode. By default, the property is set to **true**. |
| ShowPreviewZoomButtons | Enables showing the buttons to select zoom in the preview window. By default, the property is set to **true**. |


### Behavior

| **Name** | **Description** |
| --- | --- |
| ShowSaveDialog | Enables displaying the dialog to insert a report name when it is saved. The name of the report will be transferred in the parameters of the report designer. By default, the property is set to **false**. |
| SetReportModifiedWhenOpening | Specifies the report, opened when the designer runs, as already changed. By default, the property is set to **false**. |
| AllowModifyTemplate | Allows editing the loaded report template elements. Creation and editing new items will be allowed regardless of the value of the property set. By default, the property is set to **true**. |
| AutoSaveInterval | Specifies the time interval (in minutes) through which the designer automatically calls the action to save the report. The default value is set to 0 minutes (auto-saving is disabled). |
| SaveReportMode | Sets the mode to save reports. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (the default value); **Visible** - saving of the report will be called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report will be called in a new window (tab) of the web browser. |
| SaveReportAsMode | Sets the mode for saving the report. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (the default value); **Visible** - saving of the report is called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report is called in a new window (tab) of the web browser. |
| RunWizardAfterLoad | Enables displaying the window of the render report wizard when the designer runs. By default, the property is set to **false**. |
| DesignerEventFunction | Specifies the name of the JavaScript function that will be called when certain actions are taken by the designer. The function takes a string parameter to the input. The designer action ID is passed in it. |
| ExitUrl | Specifies the URL address when clicking the **Exit** button in the main menu of the designer. |


### Export options

| **Name** | **Description** |
| --- | --- |
| ShowExportDialog | Enables displaying the export options dialog box. If the property is set to **false**, the export will be performed with the default settings.. By default, the property is set to **true**. |
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


### Send report by Email

| **Name** | **Description** |
| --- | --- |
| ShowEmailDialog | Enables showing the parameters dialog for sending the report via email. If the dialog box is disabled, the email will be sent with the settings set on the server-side in the **EmailReport** action. By default, the property is set to **true**. |
| ShowEmailExportDialog | Enables showing the export parameters dialog box when sending email. If the property is **false**, the export will be done with the default settings. By default, the property is set to **true**. |
| DefaultEmailAddress | Specifies the recipient email by default. This means the address to which the email with the attached report will be sent. |


### Printing parameters

| **Name** | **Description** |
| --- | --- |
| ShowPrintDialog | Enables showing the report printing dialog box. If the print dialog is disabled, then pressing the button will immediately display the system print dialog. The report will be printed in the **Default** mode. By default, the property is set to **true**. |
| AutoPageOrientation | Enables automatic page rotation of the report, if the page orientation of the report does not match the page orientation settings of the printer.. By default, the property is set to **true**. |
| AutoPageScale | Enables automatic scaling of report page that matches the paper size. By default, the property is set to **true**. |
| AllowDefaultPrint | Enables the report printing mode - **Default** - in the print dialog box of the report preview. By default, the property is set to **true**. |
| AllowPrintToPdf | Enables the report printing mode - **Print as PDF** - in the print dialog box of the report preview. By default, the property is set to **true**. |
| AllowPrintToHtml | Enables the report printing mode - **Print as HTML** - in the print dialog box of the report preview. By default, the property is set to **true**. |
| PrintAsBitmap | Enables report printing by means of a graphical snapshot of the report page. By default, the property is set to **true**. |
