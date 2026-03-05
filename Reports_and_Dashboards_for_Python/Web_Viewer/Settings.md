# Viewer Settings

Viewer settings are configured by modifying the property values located in the main properties container named `options` of the component. All properties are divided into groups for ease of use. All enumerations used in the viewer settings are found in the namespace `stimulsoft_reports.viewer.enums`.


The example of changing some viewer settings:


**app.py**

```python

from flask import Flask, request
from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.viewer.enums import StiHtmlExportMode, StiToolbarDisplayMode, StiViewerTheme

@app.route('/viewer', methods = ['GET', 'POST'])
def viewer():
    viewer = StiViewer()
    viewer.options.localization = 'de.xml'
    viewer.options.appearance.theme = StiViewerTheme.OFFICE_2022_DARKGRAY_BLUE
    viewer.options.appearance.fullScreenMode = True
    viewer.options.appearance.scrollbarsMode = True
    viewer.options.appearance.bookmarksTreeWidth = 200
    viewer.options.toolbar.displayMode = StiToolbarDisplayMode.SEPARATED
    viewer.options.exports.showExportToWord2007 = False
    viewer.options.exports.showExportToCsv = False

    if viewer.processRequest(request):
        return viewer.getFrameworkResponse()

    # Here is the code for working with the report

    return viewer.getFrameworkResponse()
```

### Main (without group)

**Name
              
              
                Description

                width
              
              
                Sets the width of the component in "px" or "%". By default, the value is set to "100%".

                height
              
              
                Sets the height of the component in "px" or "%". By default, the value is set to "100%" for standard mode and "650px" for scroll mode.

                localization
              
              
                Sets the selected localization of the component. By default, the English localization is embedded in the component.**


### Appearance

**Name
              
              
                Description

                theme
              
              
                Sets the theme of the viewer. The list of available themes is in the StiViewerTheme enumeration. By default, the value is set to StiViewerTheme.OFFICE_2022_WHITE_BLUE.

                iconSet
              
              
                Allows setting the icon set:
                
                  StiWebUIIconSet.AUTO (default value) – automatically sets the icon set. For Office2022 themes, a Monoline icon set is used, and for Office2013 themes, a Regular icon set is used;
                  StiWebUIIconSet.MONOLINE – sets the Monoline icon set;
                  StiWebUIIconSet.REGULAR – sets the Regular icon set.

                backgroundColor
              
              
                Sets the background color of the viewer. By default, the value is 'white'.

                pageBorderColor
              
              
                Sets the page border color in the report. By default, the value is 'gray'.

                rightToLeft
              
              
                Sets the Right to Left mode for the viewer’s controls. By default, the value is set to False.

                fullScreenMode
              
              
                Sets the full-screen mode for the viewer. If this property is set to True, the width and height properties are ignored. By default, the value is set to False.

                scrollbarsMode
              
              
                Sets the mode to display the report with scrollbars. By default, the value is set to False.

                openLinksWindow
              
              
                Sets the target window or frame for opening hyperlinks from the report. By default, the value is set to 'blank' (new browser tab). It can take standard values 'blank', 'self', 'top', or a window or frame name.

                showTooltips
              
              
                Enables or disables the display of tooltips when hovering over the viewer’s tools. By default, the value is set to True.

                showTooltipsHelp
              
              
                Allows displaying or hiding a link to the documentation in the tooltips when hovering over the viewer’s tools. By default, the value is set to True.

                showDialogsHelp
              
              
                Allows displaying or hiding the help button in various menus. By default, the value is set to True.

                pageAlignment
              
              
                Sets the alignment of report pages in the viewer:
                
                  StiContentAlignmen.DEFAULT – the page alignment is determined by the template settings (default value);
                  StiContentAlignment.LEFT– pages are aligned to the left;
                  StiContentAlignment.CENTER – pages are centered;
                  StiContentAlignment.RIGHT – pages are aligned to the right.

                showPageShadow
              
              
                Enables or disables the display of page shadows in the report. By default, the value is set to False.

                bookmarksPrint
              
              
                Enables the printing of bookmarks in the report. By default, the value is set to False.

                bookmarksTreeWidth
              
              
                Sets the width of the bookmarks panel in pixels. By default, the value is set to 180.

                parametersPanelPosition
              
              
                Sets the position of the parameters panel in the viewer:
                
                  StiParametersPanelPosition.FROM_REPORT – the panel position is determined by the template settings (default value);
                
                
                  StiParametersPanelPosition.TOP - the panel is located at the top above the report page;
                  StiParametersPanelPosition.LEFT - the panel is located to the left of the report page.

                parametersPanelMaxHeight
              
              
                Sets the maximum height of the parameters panel in pixels. By default, the value is set to 300.

                parametersPanelColumnsCount
              
              
                Sets the number of columns on the parameters panel. By default, the value is set to 2.

                parametersPanelDateFormat
              
              
                Sets the date and time format for the variables displayed on the parameters panel. By default, no value is set.

                parametersPanelSortDataItems
              
              
                Enables or disables the sorting mode for the variable values. By default, the option is set to False, meaning the variable values are displayed in their original order.

                interfaceType
              
              
                Sets the viewer's interface type. The following values can be used:
                
                  StiInterfaceType.AUTO – the viewer's interface type will be automatically selected based on the device being used (default value);
                  StiInterfaceType.MOUSE – forces the use of the standard interface for controlling the viewer with a mouse;
                  StiInterfaceType.TOUCH – forces the use of the Touch interface for controlling the viewer with a touchscreen monitor; in this mode, the viewer’s interface elements are larger for ease of use;
                  StiInterfaceType.MOBILE – forces the use of the Mobile interface for controlling the viewer with a smartphone screen; in this mode, the viewer’s interface has a simplified appearance and is adapted for mobile device control.

                allowMobileMode
              
              
                Enables or disables the possibility of displaying the report or dashboard in mobile mode. If the option is set to False, the mobile view mode will not be used under any circumstances. If the option is set to True, the mobile view mode will be used when the viewer is launched on mobile devices. By default, the option is set to True.

                chartRenderType
              
              
                Sets the rendering type for charts in the report:
                
                  StiChartRenderType.ANIMATED_VECTOR – charts will be rendered in vector mode with animation (default value);
                  StiChartRenderType.VECTOR – charts will be rendered as vector images without animation.

                reportDisplayMode
              
              
                Sets the export mode for displaying report pages. It can take one of the following values:
                
                  StiHtmlExportMode.FROM_REPORT – the export mode of report elements is determined by the template settings, either Div or Table (default value);
                
                
                  StiHtmlExportMode.TABLE – report elements are exported using HTML tables;
                  StiHtmlExportMode.DIV – report elements are exported using DIV markup.

                datePickerFirstDayOfWeek
              
              
                Allows setting the first day of the week for the Date Picker tool.
                
                  StiFirstDayOfWeek.AUTO - Monday or Sunday will be set as the first day of the week based on the browser culture.
                  StiFirstDayOfWeek.MONDAY - Monday will be set as the first day of the week.
                  StiFirstDayOfWeek.SUNDAY - Sunday will be set as the first day of the week.

                datePickerIncludeCurrentDayForRanges
              
              
                Allows including or excluding the current day in the range of the Date Picker element. By default, the option is set to False, meaning the current day is not included in the range.

                appearance.allowScrollZoom
              
              
                Sets a value which allows changing the viewer’s zoom level using the mouse scroll wheel. By default the property is set to true.

                allowTouchZoom
              
              
                Enables or disables the ability to zoom the viewer by touch. By default, the option is set to True.

                combineReportPages
              
              
                Allows combining the processed report template pages into one template or presenting each template page as a separate tab in the viewer. By default, the option is set to False, meaning each template page will be presented as a separate tab in the viewer.

                allowPropagationEvents
              
              
                Allows the propagation of key press events when the report viewer is not in focus. By default, the property is set to true.

                dashboardFilterElementItemHeight
              
              
                Sets the height in pixel of the checkbox in the List Box dashboard element.**


### Toolbar

**Name
              
              
                Description

                visible
              
              
                Allows the viewer's toolbar to be shown or hidden. By default, this is set to True.  

                displayMode
              
              
                Sets the display mode of the viewer's toolbar. It can take one of the following values from the displayMode enumeration:  
                
                  StiToolbarDisplayMode.SIMPLE – simple display mode, all controls are located on a single toolbar (default value);  
                  StiToolbarDisplayMode.SEPARATED – split display mode, the toolbar is divided into upper and lower parts.  

                backgroundColor
              
              
                Allows changing the toolbar’s background color. By default, this is set to 'transparent'.  

                borderColor
              
              
                Allows changing the toolbar’s border color. By default, this is set to 'transparent'.  

                fontColor
              
              
                Allows changing the font color for all elements on the toolbar and in all menus of this toolbar. By default, this is set to 'transparent'.  

                fontFamily
              
              
                Allows changing the font for all elements on the toolbar and in all menus of this toolbar. By default, this is set to 'Arial'.  

                alignment
              
              
                Sets the alignment of elements on the toolbar:
                
                  StiContentAlignment.DEFAULT – alignment depends on the RightToLeft option (default value);
                  StiContentAlignment.LEFT – all elements will be aligned to the left of the toolbar;
                  StiContentAlignment.CENTER – all elements will be aligned to the center of the toolbar;
                  StiContentAlignment.RIGHT – all elements will be aligned to the right of the toolbar.

                showButtonCaptions
              
              
                Enables or disables the display of button captions on the viewer’s toolbar. By default, this is set to True.  

                showPrintButton
              
              
                Allows showing or hiding the Print button on the toolbar. By default, this is set to True.

                showOpenButton
              
              
                Enables the display of the Open button on the viewer's toolbar when viewing reports or dashboards. By default, this is set to True.

                showSaveButton
              
              
                Enables the display of the Save button on the viewer's toolbar when viewing reports or dashboards. By default, this is set to True.

                showSendEmailButton
              
              
                Allows showing or hiding the Send Email button on the toolbar. By default, this is set to False. Additionally, the event handler for onEmailReport must be added.

                showFindButton
              
              
                Allows showing or hiding the Find button on the toolbar. By default, this is set to True.  

                showBookmarksButton
              
              
                Allows showing or hiding the Bookmarks button on the toolbar. If this button is not displayed, the bookmarks panel in the report will not be displayed either. By default, this is set to True.  

                showParametersButton
              
              
                Allows showing or hiding the Parameters button on the toolbar. If this button is not displayed, the parameters panel in the report will not be displayed either. By default, this is set to True.  

                showResourcesButton
              
              
                Allows showing or hiding the Resources button on the toolbar. If this button is not displayed, the resources panel in the report will not be displayed either. By default, this is set to True.

                showEditorButton
              
              
                Allows showing or hiding the Editor button on the toolbar. If this button is not displayed, editable elements cannot be modified. By default, this is set to True.

                showFullScreenButton
              
              
                Enables the display of the Full Screen button on the viewer's toolbar when viewing reports or dashboards. By default, this is set to True.

                showRefreshButton
              
              
                Allows showing or hiding the Refresh button on the viewer’s toolbar when viewing dashboards. By default, this is set to True.

                showFirstPageButton
              
              
                Allows showing or hiding the First Page button on the toolbar. By default, this is set to True.

                showPreviousPageButton
              
              
                Allows showing or hiding the Previous Page button on the toolbar. By default, this is set to True.

                showCurrentPageControl
              
              
                Allows showing or hiding the Current Page indicator on the toolbar. By default, this is set to True.

                showNextPageButton
              
              
                Allows showing or hiding the Next Page button on the toolbar. By default, this is set to True.

                showLastPageButton
              
              
                Allows showing or hiding the Last Page button on the toolbar. By default, this is set to True.

                showZoomButton
              
              
                Allows showing or hiding the Zoom selection button on the toolbar. By default, this is set to True.

                showViewModeButton
              
              
                Allows showing or hiding the page view Mode button on the toolbar. By default, this is set to True.

                showDesignButton
              
              
                Enables the display of the Design button on the toolbar when viewing reports or dashboards. By default, this is set to False.

                showAboutButton
              
              
                Allows showing or hiding the About button on the toolbar. By default, this is set to True.

                showPinToolbarButton
              
              
                Allows showing or hiding the Pin button in mobile report view mode. By default, this is set to True.

                printDestination
              
              
                Sets the report print mode. It can take one of the following values from the enumeration:  
                
                  StiPrintDestination.DEFAULT – the menu with print mode options will be displayed (default);
                  StiPrintDestination.PDF – printing will be done in PDF format;
                  StiPrintDestination.DIRECT – printing will be done in HTML format directly to the printer, displaying the system print dialog;
                  StiPrintDestination.WITH_PREVIEW – printing will be done in HTML format through a pop-up report preview window.

                viewMode
              
              
                Sets the report page display mode:
                
                  StiWebViewMode.SINGLE_PAGE – a single page selected from the toolbar is displayed (default);
                  StiWebViewMode.CONTINUOUS – all report pages are displayed in a continuous scroll;
                  StiWebViewMode.MULTIPLE_PAGES – all report pages are displayed in a grid.

                zoom
              
              
                Allows setting the report page zoom level when loading the viewer. By default, this is set to 100%. The maximum value is 500%. Additionally, one of the following zoom values can be set:  
                
                  StiZoomMode.PAGE_WIDTH – zoom pages to fit page width;
                  StiZoomMode.PAGE_HEIGHT – zoom pages to fit page height.

                menuAnimation
              
              
                Enables or disables animation for displaying and closing various menus in the viewer. By default, this is set to True.  

                showMenuMode
              
              
                Sets the mode for revealing various menus in the viewer. It can take one of the following values:  
                
                  StiShowMenuMode.CLICK – menus are revealed by clicking (default);
                  StiShowMenuMode.HOVER – menus are revealed by hovering the cursor.

                autoHide
              
              
                Sets the auto-hide mode for the toolbar when viewing reports in mobile mode. By default, this is set to False.**


### Exports

**Name
              
              
                Description

                storeExportSettings
              
              
                Allows saving Export Settings in cookies. By default, the value is set to True.

                showExportDialog
              
              
                Allows displaying or hiding the Export Diallog. If the menu is hidden, the export will be executed with default values. By default, the value is set to True.

                showExportToDocument
              
              
                Allows displaying or hiding the Document File option in the Save menu. By default, the value is set to True.

                showExportToPdf
              
              
                Enables the display of the Adobe PDF File export option in the report viewer, and the Adobe PDF option in the dashboard viewer. By default, the property is set to True.

                showExportToXps
              
              
                Enables the display of the XPS File export option. By default, the property is set to True.

                showExportToPowerPoint
              
              
                Enables the display of the Microsoft PowerPoint 2007/2010 File export option. By default, the property is set to True.

                showExportToHtml
              
              
                Allows displaying or hiding the HTML File option in the Export Settings menu. By default, the value is set to True.

                showExportToHtml5
              
              
                Allows displaying or hiding the HTML5 File option in the Export Settings menu. By default, the value is set to True.

                showExportToText
              
              
                Enables the display of the Text File export option. By default, the property is set to True.

                showExportToWord2007
              
              
                Allows displaying or hiding the Microsoft Word 2007/2010 File option in the Save menu. By default, the value is set to True.

                showExportToOpenDocumentWriter
              
              
                Enables the display of the OpenDocument Writer File export option. By default, the property is set to True.

                showExportToExcel2007
              
              
                Enables the display of the Microsoft Excel 2007/2010 File export option in the report viewer, and the Microsoft Excel option in the dashboard viewer. By default, the property is set to True.

                showExportToOpenDocumentCalc
              
              
                Enables the display of the OpenDocument Calc File export option. By default, the property is set to True.

                showExportToCsv
              
              
                Enables the display of the CSV File export option. By default, the property is set to True.

                showExportToJson
              
              
                Enables the display of the Image export option, with the ability to export the report to the JSON File. By default, the property is set to False.

                showExportToImageSvg
              
              
                Enables the display of the Image export option, with the ability to export the report to the SVG file. By default, the property is set to True.

          Send by Email

                Name
              
              
                Description

                showEmailDialog
              
              
                Enables the display of the dialog box for sending the report by Email. If the dialog box is disabled, sending by Email will be done with default settings onEmailReport. By default, the value is set to True.

                showExportDialog
              
              
                Enables the display of the export settings dialog box when sending an Email. If the property is set to False, the export will be executed with default settings. By default, the value is set to True.

                defaultEmailAddress
              
              
                Sets the default recipient Email address, i.e., the address to which the email with the attached report will be sent. By default, the value isn’t set.

                defaultEmailSubject
              
              
                Sets the default subject (title) of the email. By default, the value isn’t set.

                defaultEmailMessage
              
              
                Sets the default message (text) of the email. By default, the value isn’t set.**
