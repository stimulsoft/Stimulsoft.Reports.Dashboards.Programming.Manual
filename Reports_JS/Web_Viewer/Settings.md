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

**Name
              
              
                Description

                width
              
              
                Sets the width of the component in “px” or “%”. 

                height
              
              
                Sets the height of the component in “px” or “%”. Works only in the mode if the options.appearance.scrollbarsMode property is set to true.**


### Appearance

**Name
              
              
                Description

                appearance.theme
              
              
                Specifies the theme of the viewers' layout. The list of available themes can be found in the StiViewerTheme enumeration. The default value is Office2022WhiteBlue.

                appearance.backgroundColor
              
              
                Sets the background color of the viewer. By default. it is set to Stimulsoft.System.Drawing.Color.white.

                appearance.pageBorderColor
              
              
                Sets the border color of the viewer. By default, it is set to Stimulsoft.System.Drawing.Color.gray.

                appearance.rightToLeft
              
              
                Sets the Right to Left mode for viewer controls. By default, the property is set to false.

                appearance.fullScreenMode
              
              
                Sets the full-screen display mode of the viewer. By default, the property is set to false.

                appearance.scrollbarsMode
              
              
                Sets the preview mode with scrollbars. By default, the property is set to false.

                appearance.openLinksWindow
              
              
                Sets the target window to open links contained in the report. By default, it is set to '_blank' (new window). It can have one of the standard values '_blank', '_self', '_top', as well as the name of the window or frame.

                appearance.showTooltips
              
              
                Enables displaying tips for the viewer controls when the mouse hovers over. By default, the property is set to true.

                appearance.showTooltipsHelp
              
              
                Sets a value which indicates that show or hide the help link in tooltips. By default, the property is set to true.

                appearance.showDialogsHelp
              
              
                Sets a value which indicates that show or hide the help button in dialogs. By default, the property is set to true.

                appearance.pageAlignment
              
              
                Sets the position of the report page in the viewer window. 
                
                  Stimulsoft.Viewer.StiContentAlignment.DefaultValue - page alignment is determined from the template settings (default value);
                
                
                  Stimulsoft.Viewer.StiContentAlignment.Left – the page will be aligned left;
                  Stimulsoft.Viewer.StiContentAlignment.Center – the page will be centered;
                  Stimulsoft.Viewer.StiContentAlignment.Right – the page will be aligned right.

                appearance.showPageShadow
              
              
                Enables displaying shadow for report pages. By default, the property is set to true.

                appearance.bookmarksPrint
              
              
                Enables printing of report bookmarks (besides the report itself). By default, the property is set to false.

                appearance.bookmarksTreeWidth
              
              
                Sets the width of the bookmarks panel in pixels. By default, the width is 180 pixels.

                appearance.parametersPanelMaxHeight
              
              
                Sets the maximum height of the parameters bar in pixels. By default, the maximum height is 300 pixels.

                appearance.parametersPanelColumnsCount
              
              
                Sets the number of columns to display report parameters. By default, it is set to 2 columns.

                appearance.parametersPanelSortDataItems
              
              
                Gets or sets a value which indicates that variable items will be sorted. By default the property is set to true.

                appearance.parametersPanelDateFormat
              
              
                Sets the date and time format for variables of the corresponding type in the parameters panel. By default, the property is set to String.empty.

                appearance.reportDisplayMode
              
              
                Sets the export mode for displaying report pages. It can take one of the following values of the reportDisplayMode enumeration:
                
                  FromReport - the export mode of the report elements is defined from report template settings - Div or Table (default value);
                  Table – report elements are exported using HTML tables;
                  Div – report elements are exported using DIV markup.

                appearance.interfaceType
              
              
                Sets the type of interface used for the viewer. It can take one of the following values:
                
                  Stimulsoft.Viewer.StiInterfaceType.Auto – the viewer's interface is determined automatically depending of the device that is report is displayed on (default value);
                  Stimulsoft.Viewer.StiInterfaceType.Mouse – the standard interface with a mouse control will be used for all the screen types;
                  Stimulsoft.Viewer.StiInterfaceType.Touch – the Touch interface will be used to control the viewer. The interface design was optimized for the 'touchscreen' display types. The viewer interface elements have been increased in size to simplify the control of the viewer and to improve its usability;
                  Stimulsoft.Viewer.StiInterfaceType.Mobile – the Mobile interface will be used to control the viewer for all screen types. The Mobile interface was designed to control the viewer using the mobile smartphone display. This interface design was simplified and adapted to use on smartphones. 

                appearance.allowMobileMode
              
              
                Enables or disables displaying a report or dashboard in the mobile mode. If the option is set to false, then the mobile view will not be used. If the option is set to true, the mobile view mode will be used when opening the viewer on mobile devices. By default, the option is set to true.

                appearance.chartRenderType
              
              
                Sets the chart displaying mode on the report page. 
                
                  Stimulsoft.Viewer.StiChartRenderType.AnimatedVector – charts are displayed in the vector mode as an SVG object, the chart elements are displayed with animation (set by default).
                  Stimulsoft.Viewer.StiChartRenderType.Vector – charts are displayed in the vector mode as an SVG object;

                appearance.datePickerFirstDayOfWeek
              
              
                Sets the first day of week in the date picker.
                
                  Stimulsoft.Viewer.StiFirstDayOfWeek.Auto - Sets Monday or Sunday as the first day depending on the browser culture default value);
                  Stimulsoft.Viewer.StiFirstDayOfWeek.Monday - Sets Monday as the first day of the week;
                  Stimulsoft.Viewer.StiFirstDayOfWeek.Sunday - Sets Sunday as the first day of the week.

                appearance.datePickerIncludeCurrentDayForRanges
              
              
                Sets a value, which indicates that the current day will be included in the ranges of the date picker. By default the property is set to false.

                appearance.allowScrollZoom
              
              
                Sets a value which allows changing the viewer’s zoom level using the mouse scroll wheel. By default the property is set to true.

                appearance.allowTouchZoom
              
              
                Sets a value which allows touch zoom in the viewer. By default the property is set to true.

                appearance.combineReportPages
              
              
                Sets a value which indicates that if a report contains several pages, then they will be combined in preview. By default the property is set to false.

                appearance.allowPropagationEvents
              
              
                Allows the propagation of key press events when the report viewer is not in focus. By default, the property is set to true.

                appearance.dashboardFilterElementItemHeight
              
              
                Sets the height in pixel of the checkbox in the List Box dashboard element.**


### Toolbar

**Name
              
              
                Description

                toolbar.visible
              
              
                Enables displaying the viewer toolbar. By default, the property is set to true.

                toolbar.displayMode
              
              
                Specifies the display mode of the toolbar of the viewer. It can take one of the following values of the displayMode enumeration:
                
                  Simple - all controls are located on the same control panel (default value);
                  Separated - the control panel is split into top and bottom panels.

                toolbar.backgroundColor
              
              
                Sets the color of the viewer toolbar. By default, the property is set to Stimulsoft.System.Drawing.Color.empty.

                toolbar.borderColor
              
              
                Sets the color of the borders of the Viewer toolbar. By default, the property is set to Stimulsoft.System.Drawing.Color.empty.

                toolbar.fontColor
              
              
                Sets the text color for the toolbar and the viewer menu. By default, the property is set to Stimulsoft.System.Drawing.Color.empty.

                toolbar.fontFamily
              
              
                Sets the font for the toolbar and the viewer menu.  By default, the property is set to 'Arial'.

                toolbar.alignment
              
              
                Sets the alignment mode for the controls on the viewer toolbar.
                
                  Stimulsoft.Viewer.StiContentAlignment.Default – the alignment depends on the RightToLeft property (set by default).
                  Stimulsoft.Viewer.StiContentAlignment.Left – elements will be aligned left;
                  Stimulsoft.Viewer.StiContentAlignment.Center – elements will be centered;
                  Stimulsoft.Viewer.StiContentAlignment.Right – elements will be aligned right.

                toolbar.showButtonCaptions
              
              
                Enables text of the buttons on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showOpenButton
              
              
                Enables displaying the Open button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to true.

                toolbar.showPrintButton
              
              
                Enables showing the button - Print - on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showSaveButton
              
              
                Enables displaying the Save button on the toolbar of the viewer when viewing reports or dashboards.. By default, the property is set to true.

                toolbar.showSendEmailButton
              
              
                Enables showing the button - Send Email - on the toolbar of the viewer. By default, the property is set to false. Also, you should add the onEmailReport event handler.

                toolbar.showFindButton
              
              
                Sets a visibility of the Find button in the toolbar of the viewer. By default, the property is set to true.

                toolbar.showBookmarksButton
              
              
                Enables showing the button - Bookmarks - on the toolbar of the viewer. By default, the property is set to true. If the button is hidden, the bookmarks panel will not be displayed even if there are bookmarks in the report.

                toolbar.showParametersButton
              
              
                Enables showing the button - Parameters - on the toolbar of the viewer. By default, the property is set to true. If the button is hidden, the parameters panel will not be displayed even if there are parameters in the report.

                toolbar.showResourcesButton
              
              
                Enables showing the button - Resources - on the toolbar of the viewer. By default, the property is set to true. If the button is hidden, the resources panel will not be displayed even if there are resources in the report.

                toolbar.showEditorButton
              
              
                Enables showing the button - Editor - on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showFullScreenButton
              
              
                Enables displaying the Full Screen button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to true.

                toolbar.showRefreshButton
              
              
                Sets a visibility of the Refresh button in the toolbar of the viewer. By default, the property is set to true.

                toolbar.showFirstPageButton
              
              
                Enables showing the button - First Page - on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showPreviousPageButton
              
              
                Enables showing the button - Previous Page - on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showCurrentPageControl
              
              
                Enables showing the current report page indicator. By default, the property is set to true.

                toolbar.showNextPageButton
              
              
                Enables showing the button - Next Page - on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showLastPageButton
              
              
                Enables showing the button - Last Page - on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showZoomButton
              
              
                Enables showing the Zoom button. By default, the property is set to true.

                toolbar.showViewModeButton
              
              
                Enables showing the button for selecting the display mode of report pages. By default, the property is set to true.

                toolbar.showDesignButton
              
              
                Enables displaying the Design button on the toolbar of the viewer when viewing reports or dashboards. By default, the property is set to true.

                toolbar.showAboutButton
              
              
                Enables showing the button - About - on the toolbar of the viewer. By default, the property is set to true.

                toolbar.showPinToolbarButton
              
              
                Sets a visibility of the Pin button in the toolbar of the viewer in mobile mode. By default, the property is set to true.

                toolbar.printDestination
              
              
                Sets the report printing mode. It can take one of the following values of the StiPrintDestination enumeration:
                
                  Default – a menu with a choice of printing modes will be displayed (default value);
                  Pdf – printing will be done to the PDF format;
                  Direct – printing will be done to the HTML format directly to the printer, the system print dialog will be displayed;
                  PopupWindow – printing will be done in the HTML format via the preview window of the report.

                toolbar.viewMode
              
              
                Sets the mode for displaying report pages.
                
                  Stimulsoft.Viewer.StiWebViewMode.OnePage – displays one page of the report selected in the toolbar of the viewer (the default value);
                  Stimulsoft.Viewer.StiWebViewMode.Continuous – displays all pages of the report;
                  Stimulsoft.Viewer.StiWebViewMode.MultiplePages – displays all report pages as a table.

                toolbar.zoom
              
              
                Sets the zoom for displaying report pages. The default setting is 100 percent. The values are from 10 to 500 percent. You can also set one of the following values: 
                
                  Stimulsoft.Viewer.StiZoomMode.PageWidth – when the viewer runs, the zoom, necessary to display the report by the page width, will be set;
                  Stimulsoft.Viewer.StiZoomMode.PageHeight – when the viewer runs, the zoom, required to display the page height of the report, will be set.

                toolbar.menuAnimation
              
              
                Enables animation when the viewer menu shows/hides. By default, the property is set to true.

                toolbar.showMenuMode
              
              
                Sets the display mode of the viewer menu. It can take one of the following values of the StiShowMenuMode enumeration:
                
                  Stimulsoft.Viewer.StiShowMenuMode.Click – shows menu by mouse click (default value);
                  Stimulsoft.Viewer.StiShowMenuMode.Hover – shows menu by hovering the mouse cursor.

                toolbar.autoHide
              
              
                Sets a value which allows automatically hide the viewer toolbar in mobile mode. By default, the property is set to false.**


### Exports

**Name
              
              
                Description

                export.storeExportSettings
              
              
                Sets a value which allows store the export settings in the cookies. By default, the property is set to true.

                exports.showExportDialog
              
              
                Enables showing export options dialog box. If the property is set to false, the export will be done with the default settings. By default, the property is set to true.

                exports.showExportToDocument
              
              
                Enables the export menu item - Document File. By default, the property is set to true.

                exports.showExportToPdf
              
              
                Enables displaying the Adobe PDF file export menu item when viewing reports, and the Adobe PDF item when viewing dashboards. By default, the property is set to true.

                exports.showExportToXps
              
              
                Enables the export menu item - XPS File. By default, the property is set to false.

                exports.showExportToHtml
              
              
                Enables the export menu item - HTML File. By default, the property is set to true.

                exports.showExportToHtml5
              
              
                Enables the export menu item - HTML5 File. By default, the property is set to true.

                exports.showExportToWord2007
              
              
                Enables the export menu item - Microsoft Word 2007/2010 File. By default, the property is set to true.

                exports.showExportToExcel2007
              
              
                Enables displaying the Microsoft Excel 2007/2010 File export menu item when viewing reports, and the Microsoft Excel item when viewing dashboards. By default, the property is set to true.

                exports.showExportToCsv
              
              
                Enables the export menu item - CSV. By default, the property is set to true.

                exports.showExportToJson
              
              
                Enables the export menu item - JSON. By default, the property is set to false.

                exports.showExportToText
              
              
                Enables the export menu item - Text File. By default, the property is set to true.

                exports.showExportToOpenDocumentWriter
              
              
                Enables the export menu item - OpenDocument Writer File. By default, the property is set to true.

                exports.showExportToOpenDocumentCalc
              
              
                Enables the export menu item - OpenDocument Calc File. By default, the property is set to true.

                exports.showExportToPowerPoint
              
              
                Enables the export menu item - Microsoft PowerPoint File. By default, the property is set to true.

                exports.showExportToImageSvg
              
              
                Enables displaying the Image export menu item, with the ability to export the report to an SVG file. By default, the property is set to true.

          Email

                      Name
                    
                    
                      Description

                      email.showEmailDialog
                    
                    
                      Enables displaying settings for sending the report via email. If the dialog box is disabled, the email will be sent with the settings set on the server side in the onEmailReport event. By default, the property is set to true.

                      email.showExportDialog
                    
                    
                      Enables displaying export options dialog box when sending email. If the property is set to false, the export will be done with the default settings. By default, the property is set to true.

                      email.defaultEmailAddress
                    
                    
                      Sets the default recipient email, i.e. the address to which the email with the attached report will be sent.

                      email.defaultEmailSubject
                    
                    
                      Sets the default email subject (header).

                      email.defaultEmailMessage
                    
                    
                      Sets the default email message (text).**
