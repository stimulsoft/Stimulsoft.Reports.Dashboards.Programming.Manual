# Viewer Settings

The **HTML5 Viewer** is configured using properties that are located in the **Stimulsoft.Viewer.StiViewerOptions** class. All properties are divided into groups. Some of the groups contain subgroups for ease of use. The following is an example of setting the properties of the viewer.


**viewer.html**

```html
...
<script type="text/javascript">
    var report = new Stimulsoft.Report.StiReport();
    report.loadFile("SimpleList.mrt");
    
    var options = new Stimulsoft.Viewer.StiViewerOptions();
    
    options.width = "1000px";
    options.height = "1000px";
    
    options.appearance.theme = Stimulsoft.Viewer.StiViewerTheme.Office2022WhiteBlue;
    options.appearance.reportDisplayMode = Stimulsoft.Report.Export.StiHtmlExportMode.Div;
    options.appearance.scrollbarsMode = true;
    options.appearance.backgroundColor = Stimulsoft.System.Drawing.Color.dodgerBlue;
    options.appearance.showTooltips = false;
    
    options.toolbar.showPrintButton = false;
    options.toolbar.showDesignButton = false;
    options.toolbar.showAboutButton = false;
    
    options.exports.showExportToPdf = true;
    options.exports.ShowExportToWord2007 = true;
    
    var viewer = new Stimulsoft.Viewer.StiViewer(options);
    viewer.report = report;
</script>
...
```

Please note that all dashboard elements have their own save options and full-screen buttons for preview. There are no special options to control displaying them, but they can be disabled through the properties of the element. The code below should be added after loading the report before passing it to the viewer.


**Default.aspx.cs**

```csharp
...
var dbsElementInteraction = report.getComponentByName("RegionMap1").dashboardInteraction;
    dbsElementInteraction.showFullScreenButton = false;
    dbsElementInteraction.showSaveButton = false;
...
```

### Main settings (without groups)


| **Name** | **Description** |
| --- | --- |
| `width` | Sets the width of the component in “px” or “%”. |
| `height` | Sets the height of the component in “px” or “%”. Works only in the mode if the `options.appearance.scrollbarsMode` property is set to `true`. |
| `localization` | Sets the selected localization of the component. By default, the English localization is set. It is built into the component. |

### Appearance


| **Name** | **Description** |
| --- | --- |
| `theme` | Specifies the theme of the viewers' layout. The list of available themes can be found in the `StiViewerTheme` enumeration. The default value is `Office2022WhiteBlue`. |
| `iconSet` | Allows setting the icon set: `StiWebUIIconSet.Auto` - automatically sets the icon set. For **Office2022** themes, the **Monoline** icon set is used, and for **Office2013** themes, the **Regular** icon set is used; `StiWebUIIconSet.Monoline` - sets the **Monoline** style icon set; `StiWebUIIconSet.Regular` - sets the **Regular** style icon set. By default, the property is set to `StiWebUIIconSet.Auto`. |
| `backgroundColor` | Sets the background color of the viewer. By default. it is set to `Stimulsoft.System.Drawing.Color.white`. |
| `pageBorderColor` | Sets the border color of the viewer. By default, it is set to `Stimulsoft.System.Drawing.Color.gray`. |
| `rightToLeft` | Sets the **Right to Left** mode for viewer controls. By default, the property is set to `false`. |
| `fullScreenMode` | Sets the viewer display to fullscreen mode. If the property is set to `true`, the values of the **width** and **height** properties are ignored. By default, the value is set to `false`. |
| `scrollbarsMode` | Sets the preview mode with scrollbars. By default, the property is set to `false`. |
| `openLinksWindow` | Sets the target window to open links contained in the report. By default, it is set to ' `blank`' (a new window). It can have one of the standard values ' `blank`', '`_self`', '`_top`', as well as the name of the window or frame. |
| `openExportedReportWindow` | Sets the target window or frame for opening the exported report. By default, the value is set to ' `blank`' (a new browser tab). It can accept one of the standard values: ' `blank`', ' `self`', ' `top`', as well as a custom window or frame name. |
| `showTooltips` | Enables displaying tips for the viewer controls when the mouse hovers over. By default, the property is set to `true`. |
| `showTooltipsHelp` | Sets a value which indicates that show or hide the help link in tooltips. By default, the property is set to `true`. |
| `showDialogsHelp` | Sets a value which indicates that show or hide the help button in dialogs. By default, the property is set to `true`. |
| `pageAlignment` | Sets the position of the report page in the viewer window: `StiContentAlignment.`DefaultValue - page alignment is determined from the template settings (default value); `StiContentAlignment.Left` – the page will be aligned left; `StiContentAlignment.Center` – the page will be centered; `StiContentAlignment.Right` – the page will be aligned right. By default, the property is set to `StiContentAlignment.`DefaultValue. |
| `showPageShadow` | Enables displaying shadow for report pages. By default, the property is set to `true`. |
| `bookmarksPrint` | Enables printing of report bookmarks (besides the report itself). By default, the property is set to `false`. |
| `bookmarksTreeWidth` | Sets the width of the bookmarks panel in pixels. By default, the width is 180 pixels. |
| `parametersPanelPosition` | It sets location of the panel parameters in the viewer: `StiParametersPanelPosition.FromReport` - the location of the panel is determined from the template settings; `StiParametersPanelPosition.Top` - the panel is located upper report page; `StiParametersPanelPosition.Left` - the panel is located to the left from report page. By default, the property is set to `StiParametersPanelPosition.FromReport`. |
| `parametersPanelMaxHeight` | Sets the maximum height of the parameters bar in pixels. By default, the maximum height is 300 pixels. |
| `parametersPanelColumnsCount` | Sets the number of columns to display report parameters. By default, it is set to 2 columns. |
| `minParametersCountForMultiColumns` | Sets the minimum number of variables on the parameters panel for multi-column display mode. The default value is 5. |
| `parametersPanelSortDataItems` | Gets or sets a value which indicates that variable items will be sorted. By default the property is set to `true`. |
| `parametersPanelDateFormat` | Sets the date and time format for variables of the corresponding type in the parameters panel. By default, no value is specified. |
| `parametersPanelShowDescriptions` | Gets or sets a value which indicates that showing descriptions for variables is allowed. By default, the property is set to `true`. |
| `reportDisplayMode` | Sets the export mode for displaying report pages. It can take one of the following values of the `reportDisplayMode` enumeration: `StiHtmlExportMode.FromReport` - the export mode of the report elements is defined from report template settings Div or Table; `StiHtmlExportMode.Table` - report elements are exported using HTML tables; `StiHtmlExportMode.Span` – report elements are exported using HTML Span tags with absolute positioning of elements; `StiHtmlExportMode.Div` – report elements are exported using DIV markup. By default, the property is set to `StiHtmlExportMode.FromReport`. |
| `interfaceType` | Sets the type of interface used for the viewer. It can take one of the following values: `StiInterfaceType.Auto` – the viewer's interface is determined automatically depending of the device that is report is displayed on; `StiInterfaceType.Mouse` – the standard interface with a mouse control will be used for all the screen types; `StiInterfaceType.Touch` – the Touch interface will be used to control the viewer. The interface design was optimized for the 'touchscreen' display types. The viewer interface elements have been increased in size to simplify the control of the viewer and to improve its usability; `StiInterfaceType.Mobile` – the Mobile interface will be used to control the viewer for all screen types. The Mobile interface was designed to control the viewer using the mobile smartphone display. This interface design was simplified and adapted to use on smartphones. By default, the property is set to `StiInterfaceType.Auto`. |
| `allowMobileMode` | Enables or disables displaying a report or dashboard in the mobile mode. If the option is set to `false`, then the mobile view will not be used. If the option is set to `true`, the mobile view mode will be used when opening the viewer on mobile devices. By default, the option is set to `true`. |
| `chartRenderType` | Sets the chart displaying mode on the report page: `StiChartRenderType.AnimatedVector` – charts are displayed in the vector mode as an SVG object, the chart elements are displayed with animation; `StiChartRenderType.Vector` – charts are displayed in the vector mode as an SVG object. By default, the property is set to `StiChartRenderType.AnimatedVector`. |
| `datePickerFirstDayOfWeek` | Sets the first day of week in the date picker: `StiFirstDayOfWeek.Auto`- Sets **Monday** or **Sunday** as the first day depending on the browser culture default value); `StiFirstDayOfWeek.Monday` - Sets **Monday** as the first day of the week; `StiFirstDayOfWeek.Sunday` - Sets **Sunday** as the first day of the week. By default, the property is set to `Stimulsoft.Viewer.StiFirstDayOfWeek.Auto`. |
| `datePickerIncludeCurrentDayForRanges` | Sets a value, which indicates that the current day will be included in the ranges of the date picker. By default the property is set to `false`. |
| `allowScrollZoom` | Sets a value which allows changing the viewer’s zoom level using the mouse scroll wheel. By default the property is set to `true`. |
| `allowTouchZoom` | Sets a value which allows touch zoom in the viewer. By default the property is set to `true`. |
| `combineReportPages` | Sets a value which indicates that if a report contains several pages, then they will be combined in preview. By default the property is set to `false`. |
| `allowPropagationEvents` | Allows the propagation of key press events when the report viewer is not in focus. By default, the property is set to `true`. |
| `dashboardFilterElementItemHeight` | Sets the height in pixel of the checkbox in the **List Box** dashboard element. |
| `allowLoadingFilterItemsOnScroll` | Provides the ability to load dashboard filter elements while scrolling. By default, the property is set to `false`. |

### Toolbar


| **Name** | **Description** |
| --- | --- |
| `visible` | Enables displaying the viewer toolbar. By default, the property is set to `true`. |
| `displayMode` | Specifies the display mode of the toolbar of the viewer. It can take one of the following values of the `displayMode` enumeration: `StiToolbarDisplayMode.Auto -`the toolbar display mode is determined automatically depending on the device, screen size, and report viewing mode; `StiToolbarDisplayMode.Simple` - all controls are located on the same control panel (default value); `StiToolbarDisplayMode.SimpleDocked`- the toolbar is displayed in a simplified docked mode with a minimal set of controls; `StiToolbarDisplayMode.Separated` - the control panel is split into top and bottom panels. By default, the property is set to `StiToolbarDisplayMode.Auto`. |
| `backgroundColor` | Sets the color of the Viewer toolbar. By default, the property is set to `Stimulsoft.System.Drawing.Color.empty`. |
| `borderColor` | Sets the color of the borders of the Viewer toolbar. By default, the property is set to `Stimulsoft.System.Drawing.Color.empty`. |
| `fontColor` | Sets the text color for the toolbar and the viewer menu. By default, the property is set to `Stimulsoft.System.Drawing.Color.empty`. |
| `fontFamily` | Sets the font for the toolbar and the viewer menu.  By default, the property is set to `Arial`. |
| `alignment` | Sets the alignment mode for the controls on the viewer toolbar: `StiContentAlignment.Default` – the alignment depends on the `RightToLeft` property; `StiContentAlignment.Left` – elements will be aligned left; `StiContentAlignment.Center` – elements will be centered; `StiContentAlignment.Right` – elements will be aligned right. By default, the property is set to`StiContentAlignment.Default`. |
| `showButtonCaptions` | Enables text of the buttons on the toolbar of the viewer. By default, the property is set to `true`. |
| `showOpenButton` | Enables displaying the **Open** button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to `true`. |
| `showPrintButton` | Enables showing the **Print** button  on the toolbar of the viewer. By default, the property is set to `true`. |
| `showSaveButton` | Enables displaying the **Save** button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to `true`. |
| `showSendEmailButton` | Enables showing the **Send Email** button on the toolbar of the viewer. By default, the property is set to `false`. Also, you should [add the onEmailReport event handler](Send_Email.md). |
| `showFindButton` | Sets a visibility of the **Find** button in the toolbar of the viewer. By default, the property is set to `true`. |
| `showSignatureButton` | Provides the ability to show or hide the **Signature** button on the toolbar. By default, the value is set to `true`. |
| `showBookmarksButton` | Enables showing the **Bookmarks** button on the toolbar of the viewer. By default, the property is set to `true`. If the button is hidden, the bookmarks panel will not be displayed even if there are bookmarks in the report. |
| `showBookmarksPanel` | Gets or sets a value indicating whether the **Bookmarks** panel is shown automatically when the report has bookmarks. Default value is `true`. |
| `showParametersButton` | Enables showing the **Parameters** button on the toolbar of the viewer. By default, the property is set to `true`. If the button is hidden, the parameters panel will not be displayed even if there are parameters in the report. |
| `showResourcesButton` | Enables showing the **Resources** button on the toolbar of the viewer. By default, the property is set to `true`. If the button is hidden, the resources panel will not be displayed even if there are resources in the report. |
| `showEditorButton` | Enables showing the **Editor** button on the toolbar of the viewer. By default, the property is set to `true`. |
| `showFullScreenButton` | Enables displaying the **Full Screen** button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to `true`. |
| `showRefreshButton` | Sets a visibility of the **Refresh** button in the toolbar of the viewer. By default, the property is set to `true`. |
| `showFirstPageButton` | Enables showing the **First Page** button on the toolbar of the viewer. By default, the property is set to `true`. |
| `showPreviousPageButton` | Enables showing the **Previous Page** button on the toolbar of the viewer. By default, the property is set to `true`. |
| `showCurrentPageControl` | Enables showing the current report page indicator. By default, the property is set to `true`. |
| `showNextPageButton` | Enables showing the **Next Page** button on the toolbar of the viewer. By default, the property is set to `true`. |
| `showLastPageButton` | Enables showing the **Last Page** button on the toolbar of the viewer. By default, the property is set to `true`. |
| `showZoomButton` | Enables showing the **Zoom** button. By default, the property is set to `true`. |
| `showViewModeButton` | Enables showing the button for selecting the display mode of report pages. By default, the property is set to `true`. |
| `showDesignButton` | Enables displaying the **Design** button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to `true`. |
| `showAboutButton` | Enables showing the **About** button on the toolbar of the viewer. By default, the property is set to `true`. |
| `showPinToolbarButton` | Sets a visibility of the **Pin** button in the toolbar of the viewer in mobile mode. By default, the property is set to `true`. |
| `printDestination` | Sets the report printing mode. It can take one of the following values of the `StiPrintDestination` enumeration: `StiPrintDestination.Default` – a menu with a choice of printing modes will be displayed; `StiPrintDestination.Pdf` – printing will be done to the PDF format; `StiPrintDestination.Direct` – printing will be done to the HTML format directly to the printer, the system print dialog will be displayed; `StiPrintDestination.WithWindow`– printing will be done in the HTML format via the preview window of the report. By default, the property is set to `StiPrintDestination.Default`. |
| `viewMode` | Sets the mode for displaying report pages: `StiWebViewMode.OnePage` – displays one page of the report selected in the toolbar of the viewer; `StiWebViewMode.Continuous` – displays all pages of the report; `StiWebViewMode.MultiplePages` – displays all report pages as a table; `StiWebViewMode.SinglePage -`only one report page is displayed in the viewer area. Navigation between pages is performed using the navigation panel; `StiWebViewMode.WholeReport -` all report pages are displayed sequentially in the viewer area as a single continuous ribbon. By default, the property is set to `StiWebViewMode.SinglePage`. |
| `multiPageWidthCount` | Sets the number of report pages displayed horizontally in `MultiplePages` mode. By default, the value is set to 2 pages. |
| `multiPageHeightCount` | Sets the number of report pages displayed vertically in `MultiplePages` mode. By default, the value is set to 2 pages. |
| `zoom` | Sets the zoom for displaying report pages. You can also set one of the following values: `StiZoomMode.PageWidth`– when the viewer runs, the zoom, necessary to display the report by the page width, will be set; `StiZoomMode.PageHeight` – when the viewer runs, the zoom, required to display the page height of the report, will be set. The default setting is 100 percent. The values are from 10 to 500 percent. |
| `menuAnimation` | Enables animation when the viewer menu shows/hides. By default, the property is set to `true`. |
| `showMenuMode` | Sets the display mode of the viewer menu. It can take one of the following values of the `StiShowMenuMode` enumeration: `StiShowMenuMode.Click` – shows menu by mouse click; `StiShowMenuMode.Hover` – shows menu by hovering the mouse cursor. By default, the property is set to `StiShowMenuMode.Click.` |
| `autoHide` | Sets a value which allows automatically hide the viewer toolbar in mobile mode. By default, the property is set to `false`. |

### Exports


| **Name** | **Description** |
| --- | --- |
| `storeExportSettings` | Sets the ability to save export settings in cookies. By default, the value is set to `true`. |
| `showExportDialog` | Enables showing export options dialog box. If the property is set to `false`, the export will be done with the default settings. By default, the property is set to `true`. |
| `showExportToDocument` | Enables the export menu item the **Document File**. By default, the property is set to `true`. |
| `showExportToPdf` | Enables displaying the **Adobe PDF file** export menu item when viewing reports, and the **Adobe PDF** item when viewing dashboards. By default, the property is set to `true`. |
| `showExportToXps` | Enables the export menu item **XPS File**. By default, the property is set to `false`. |
| `showExportToPowerPoint` | Enables the export menu item **Microsoft PowerPoint File**. By default, the property is set to `true`. |
| `showExportToHtml` | Enables the export menu item **HTML File**. By default, the property is set to `true`. |
| `showExportToHtml5` | Enables the export menu item **HTML5 File**. By default, the property is set to `true`. |
| `showExportToText` | Enables the export menu item **Text File**. By default, the property is set to `true`. |
| `showExportToWord` | It enables the display of the the **Microsoft Word** export menu item. The property has the `true` value by default. |
| `showExportToOpenDocumentWriter` | Enables the export menu item **OpenDocument Writer** **File**. By default, the property is set to `true`. |
| `showExportToExcel` | It enables the display of the **Microsoft Word** export menu item. The property has the `true` value by default. |
| `showExportToOpenDocumentCalc` | Enables the export menu item **OpenDocument Calc** **File**. By default, the property is set to `true`. |
| `showExportToCsv` | Enables the display of the CSV File export menu item. By default, the property is set to true. |
| `showExportToJson` | Enables the export menu item **JSON**. By default, the property is set to `false`. |
| `showExportToDbf` | Enables the display of the **DBF** type in the settings of the **Data** export menu item. By default, the property is set to `true`. |
| `showExportToXml` | Enables the display of the **XML** type in the settings of the **Data** export menu item. By default, the property is set to `true`. |
| `showExportToDif` | Enables the display of the **DIF** type in the settings of the **Data** export menu item. By default, the property is set to `true`. |
| `showExportToSylk` | Enables the display of the **SYLK** type in the settings of the **Data** export menu item. By default, the property is set to `true`. |
| `showExportToImageSvg` | Enables displaying the **Image** export menu item, with the ability to export the report to an **SVG** file. By default, the property is set to `true`. |
| `showExportToImagePng` | It enables display of the **PNG** type in the settings of the **Image** export menu item. By default, the property is set to `true`. |
| `showExportToImageJpeg` | Enables the display of the **JPEG** type in the settings of the **Image** export menu item. By default, the property is set to `true`. |
| `showExportToImageSvgz` | Enables the display of the **SVGZ** type in the settings of the **Image** export menu item. By default, the property is set to `true`. |
| `showExportToImagePcx` | Enables the display of the **PCX** type in the settings of the **Image** export menu item. By default, the property is set to `true`. |
| `showExportToImageBmp` | Enables the display of the **BMP** type in the settings of the **Image** export menu item. By default, the property is set to `true`. |
| `showExportToImageGif` | Enables the display of the **GIF** type in the settings of the **Image** export menu item. By default, the property is set to `true`. |
| `showExportToImageTiff` | Enables the display of the **TIFF** type in the settings of the **Image** export menu item. By default, the property is set to `true`. |
| `showExportDataOnly` | Enables the display of the **Export Data Only** option in the settings of the **Data** export menu item. By default, the property is set to `true`. |
| `showExportToRtf` | Enables the display of the **RTF** export menu item. By default, the property is set to `true`. |

**Email**


| **Name** | **Description** |
| --- | --- |
| `showEmailDialog` | Enables displaying settings for sending the report via email. If the dialog box is disabled, the email will be sent with the settings set on the server side in the `onEmailReport` event. By default, the property is set to `true`. |
| `showExportDialog` | Enables displaying export options dialog box when sending email. If the property is set to `false`, the export will be done with the default settings. By default, the property is set to `true`. |
| `defaultEmailAddress` | Sets the default recipient email, i.e. the address to which the email with the attached report will be sent. |
| `defaultEmailSubject` | Sets the default email subject (header). |
| `defaultEmailMessage` | Sets the default email message (text). |
