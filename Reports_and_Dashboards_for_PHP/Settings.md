# Viewer Settings

The viewer is configured by modifying the values of properties located in the main `options` property container of the component. All properties are divided into groups for ease of use.


Example of setting some viewer properties:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Viewer\Enums\StiToolbarDisplayMode;
    use Stimulsoft\Viewer\Enums\StiViewerTheme;
    use Stimulsoft\Viewer\Enums\StiHtmlExportMode;
    
    $viewer = new StiViewer();
    $viewer->options->appearance->theme = StiViewerTheme::Office2022WhiteGreen;
    $viewer->options->appearance->reportDisplayMode = StiHtmlExportMode::FromReport;
    $viewer->options->width = '1000px';
    $viewer->options->height = '1000px';
    $viewer->options->toolbar->displayMode = StiToolbarDisplayMode::Separated;
    $viewer->options->toolbar->zoom = 50;
    $viewer->options->appearance->fullScreenMode = true;
    $viewer->options->appearance->scrollbarsMode = true;
    $viewer->options->exports->ShowExportToWord = false;
    $viewer->options->exports->showExportToCsv = false;
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).

### Main settings (without groups)

**Name
              
              
                Description

                width
              
              
                Sets the width of the component in “px” or “%”. The "100%" value is set by default.

                height
              
              
                It sets height of a component in "px" or "%". The "100%" value is set by default for standard mode and "650px" for the mode of display with scroll bars. 

                localization
              
              
                Sets the selected localization of the component. By default, the English localization is set. It is built into the component.**


### Appearance

**Name
              
              
                Description

                theme
              
              
                Sets the theme of the viewer. The list of available themes can be found in the StiViewerTheme enumeration. The default value is StiViewerTheme::Office2022WhiteBlue.

                iconSet
              
              
                Allows setting the icon set:
                
                  StiWebUIIconSet::Auto (default) - automatically sets the icon set. For Office2022 themes, the Monoline icon set is used, and for Office2013 themes, the Regular icon set is used;
                  StiWebUIIconSet::Monoline - sets the Monoline style icon set;
                  StiWebUIIconSet::Regular - sets the Regular style icon set.

                backgroundColor
              
              
                Sets the background color of the viewer. By default. it is set to 'white'.

                pageBorderColor
              
              
                Sets the border color of the viewer. By default, it is set to 'gray'.

                rightToLeft
              
              
                Sets the Right to Left mode for viewer controls. By default, the property is set to false.

                fullScreenMode
              
              
                It sets the full screen mode of the viewer display. If the property is set in the true value, the values of width and height properties are ignored. The false value is set by dedault.

                scrollbarsMode
              
              
                Sets the preview mode with scrollbars. By default, the property is set to false.

                openLinksWindow
              
              
                Sets the target window to open links contained in the report. By default, it is set to '_blank' (new window). It can have one of the standard values '_blank', '_self', '_top', as well as the name of the window or frame.

                openExportedReportWindow
              
              
                Sets the target window or frame for opening the exported report. The default is '_blank' (new browser tab). It can take one of the standard values: '_blank', '_self', '_top', or the name of a window or frame.

                showTooltips
              
              
                Enables displaying tips for the viewer controls when the mouse hovers over. By default, the property is set to true.

                showTooltipsHelp
              
              
                Sets a value which indicates that show or hide the help link in tooltips. By default, the property is set to true.

                showDialogsHelp
              
              
                Sets a value which indicates that show or hide the help button in dialogs. By default, the property is set to true.

                pageAlignment
              
              
                Sets the position of the report page in the viewer window:
                
                  StiContentAlignment::DefaultValue - page alignment is determined from the template settings (value is set by default);
                
                
                  StiContentAlignment::Left – the page will be aligned left;
                  StiContentAlignment::Center – the page will be centered (set by default);
                  StiContentAlignment::Right – the page will be aligned right.

                showPageShadow
              
              
                Enables displaying shadow for report pages. By default, the property is set to false.

                bookmarksPrint
              
              
                Enables printing of report bookmarks (besides the report itself). By default, the property is set to false.

                bookmarksTreeWidth
              
              
                Sets the width of the bookmarks panel in pixels. By default, the width is 180 pixels.

                parametersPanelPosition
              
              
                It sets location of the panel parameters in the viewer:
                
                  StiParametersPanelPosition::FromReport - the location of the panel is determined from the template settings (value is set by default);
                  StiParametersPanelPosition::Top - the panel is located upper report page;
                  StiParametersPanelPosition::Left - the panel is located to the left from report page.

                parametersPanelMaxHeight
              
              
                It sets max height of the parameter panel in pixels. The 300 value is set by default.

                parametersPanelColumnsCount
              
              
                It sets the number of columns in the parameter panel. The 2 value is set by default.

                minParametersCountForMultiColumns
              
              
                Sets the minimum number of variables on the parameters panel for multi-column display mode. The default value is 5.

                parametersPanelDateFormat
              
              
                It sets date and time format for the variables, which are displayed in the parameter panel. The String.empty value is set by default.  

                parametersPanelSortDataItems
              
              
                It sets or disables the sorting variable values mode. The option is set in the true value by default, i.e variable values are sorted.   

                interfaceType
              
              
                It sets the type of the viewer interface. The following values can be used:
                
                  StiInterfaceType::Auto – the type of the viewer interface will be selected automatically depending on the device you use (value is set by default);
                  StiInterfaceType::Mouse – forced using of standard interface to control the viewer using a computer mouse;
                  StiInterfaceType::Touch – forced using the Touch interface to control the viewer using touch screen of a monitor. In this mode, the viewer interface elements have enlarged sizes for comfortable control;
                  StiInterfaceType::Mobile – forced using the Mobile interface to control the viewer using smartphone screen. In this mode, the viewer interface has a simplified appearance to control using a mobile device.

                allowMobileMode
              
              
                Enables or disables displaying a report or dashboard in the mobile mode. If the option is set to false, then the mobile view will not be used. If the option is set to true, the mobile view mode will be used when opening the viewer on mobile devices. By default, the option is set to true.

                chartRenderType
              
              
                It sets the type of chart drawing in a report:
                
                  StiChartRenderType::AnimatedVector – charts will be drawn in the vector mode with animation (value is set by default);
                  StiChartRenderType::Vector – charts will be drawn as a vector image without animation.

                reportDisplayMode
              
              
                It sets the export mode to display report pages. It can take one of the following values:
                
                  StiHtmlExportMode::FromReport - the export mode of the report elements is defined from report template settings - Div or Table (value is set by default);
                
                
                  StiHtmlExportMode::Table – report elements are exported using HTML tables;
                  StiHtmlExportMode::Div – report elements are exported using DIV markup.

                datePickerFirstDayOfWeek
              
              
                It gives an ability to set the first day of the week for the Date Picker tool:
                
                  StiFirstDayOfWeek::Auto - Monday or Sunday will be set as the first day of the week depending on browser culture (value is set by default);
                  StiFirstDayOfWeek::Monday - Monday will be set as the first day of the week;
                  StiFirstDayOfWeek::Sunday - Sunday will be set as the first day of the week.

                datePickerIncludeCurrentDayForRanges
              
              
                It gives an ability to include or not the current day into the range of the Date Picker element values. By default, the option is set in the false value i.e. the current day is not included into the range of the element values.

                appearance.allowScrollZoom
              
              
                Sets a value which allows changing the viewer’s zoom level using the mouse scroll wheel. By default the property is set to true.

                allowTouchZoom
              
              
                It gives an ability change the viewer zoom by touching. By default, the option is set in the true value. 

                combineReportPages
              
              
                It allows you to combine processed pages of report template into one template or present each page of the template as a separate tab in the viewer. By default, the option is set in the false value i.e. each page of report template will be presented as a separate tab in the viewer. 

                allowPropagationEvents
              
              
                Allows the propagation of key press events when the report viewer is not in focus. By default, the property is set to true.

                dashboardFilterElementItemHeight
              
              
                Sets the height in pixel of the checkbox in the List Box dashboard element.**


### Toolbar

**Name
              
              
                Description

                visible
              
              
                It allows you to display or not to display the viewer toolbar. By default, the true value is set. 

                displayMode
              
              
                It sets the display of the viewer toolbar. It can take one of the enumeration values below:
                
                  StiToolbarDisplayMode::Simple – simple display mode, all elements of control are located in one control panel (value is set by default);
                  StiToolbarDisplayMode::Separated – separated display mode, toolbar is divided into upper and bottom.

                backgroundColor
              
              
                It allows you to change the color of toolbar. The 'transparent' value is set by default. 

                borderColor
              
              
                It allows you to change toolbar border color. The 'transparent' value is set by default.

                fontColor
              
              
                It gives an ability to change the font of all elements in the toolbar and in all menus of this panel. The 'transparent' value is set by default.

                fontFamily
              
              
                It allows you to change the font for all elements in the toolbar and in all menus of this panel. By default, the 'Arial' value is set.

                alignment
              
              
                It sets the alignment of elements in the control panel: 
                
                  StiContentAlignment::Default – alignment of elements depends on the RightToLeft option (value is set by default);
                  StiContentAlignment::Left – all elements will be aligned to the left side of the toolbar;
                  StiContentAlignment::Center – all elements will be aligned to the center of the toolbar;
                  StiContentAlignment::Right – all elements will be aligned to the right side of the toolbar.

                showButtonCaptions
              
              
                It enables or disables the display of the viewer toolbar buttons text. By default, the property is set to true.

                showPrintButton
              
              
                It allows you to display or not to display the Print button. By default, the property is set to true.

                showOpenButton
              
              
                It enables the display of the Open button in the viewer toolbar when viewing reports or dashboards. By default, the property is set to true.

                showSaveButton
              
              
                It enables the display of the Save button in the toolbar when viewing reports or dashboards. By default, the property is set to true.

                showSendEmailButton
              
              
                It allows you to display or not to display the Send Email button in the toolbar. By default, the false value is set. Also, you should add the onEmailReport event handler. 

                showFindButton
              
              
                It allows you to display or not to display the Find button in the toolbar. By default, the property is set to true.

                showSignatureButton

                showBookmarksButton
              
              
                It allows you to display or not to display the Bookmarks button in the toolbar. If this button is not displayed, the bookmark panel, the bookmark panel will not be displayed in a report. By default, the property is set to true.

                showParametersButton
              
              
                It allows you to display or not to display the Parameters button in the toolbar. If this button is not displayed, the parameter panel will not be displayed in a report. By default, the property is set to true.

                showResourcesButton
              
              
                It allows you to display or not to display the Resources button in the toolbar. If this button is not displayed, the resources panel will not be displayed in a report. By default, the property is set to true.

                showEditorButton
              
              
                It allows you to display or not to display the Editor button in the toolbar. If this button is not displayed, you won't be able to change edited data. By default, the property is set to true.

                showFullScreenButton
              
              
                It enables the display of the Full Screen button in the viewer toolbar when viewing reports or dashboards. By default, the property is set to true.

                showRefreshButton
              
              
                It allows you to display or not to display the Refresh button in the viewer toolbar when viewing dashboards. By default, the property is set to true.

                showFirstPageButton
              
              
                It allows you to display or not to display the First Page button in the toolbar. By default, the property is set to true.

                showPreviousPageButton
              
              
                It allows you to display or not to display the Previous Page in the toolbar.By default, the property is set to true.

                showCurrentPageControl
              
              
                It allows you to display or not to display an indicator of the current page in the toolbar.By default, the property is set to true.

                showNextPageButton
              
              
                It allows you to display or not to display the Next Page button in the toolbar. By default, the property is set to true.

                showLastPageButton
              
              
                It allows you to display or not to display the Last Page button in the toolbar. By default, the property is set to true.

                showZoomButton
              
              
                It allows you to display or not to display the Zoom selection button in the toolbar. By default, the property is set to true.

                showViewModeButton
              
              
                It allows you to display or not to display the report pages display modes button. By default, the property is set to true.

                showDesignButton
              
              
                It enables the display of the Design button in the viewer toolbar when viewing reports or dashboards. By default, the property is set to false.

                showAboutButton
              
              
                It allows you to display or not to display the About button. By default, the property is set to true.

                showPinToolbarButton
              
              
                It allows you to display or not to display the Pin button in the mobile mode of report viewing. By default, the property is set to true.

                printDestination
              
              
                It sets the report print mode. It can take one of the enumeration values below:
                
                  StiPrintDestination::Default – the menu with the selection print mode will be displayed (value is set by default);
                  StiPrintDestination::Pdf – print will be made in PDF format;
                  StiPrintDestination::Direct – print will be made in HTML format directly to the printer. System print dialog will be displayed;
                  StiPrintDestination::PopupWindow – print will be made in HTML format via the pop-up window of report preview.

                viewMode
              
              
                It sets the report pages display mode:
                
                  StiWebViewMode::OnePage – one page selected in the toolbar is displayed (value is set by default);
                  StiWebViewMode::Continuous – all report pages are displayed as a ribbon;
                  StiWebViewMode::MultiplePages – all report pages are displayed as a table.

                zoom
              
              
                It allows you to set the scale of report pages when loading the viewer. 100 percent by default. Max value is 500 percent.
                
                  StiZoomMode::PageWidth – report pages scale by page width;
                  StiZoomMode::PageHeight – report pages scale by page height.

                menuAnimation
              
              
                It allows you to enable or disable the animation of display and closing various menus in the viewer. By default, the property is set to true.

                showMenuMode
              
              
                It sets the mode opening of various menus in the viewer when hovering or clicking. 
                
                  StiShowMenuMode::Click – click-to-open menu mode (value is set by default);
                  StiShowMenuMode::Hover – hover-to-open menu mode.

                autoHide
              
              
                It sets the mode of automatic collapsing the toolbar when viewing a report in the mobile mode. By default, the property is set to true.**


### Exports

**Name
              
              
                Description

                storeExportSettings
              
              
                It allows you to save export settings in cookies. The true value is set by default. 

                showExportDialog
              
              
                It allows you to display or not to display the Export Settings menu. If the menu is hidden, the export will be made with values by default. The true value is set by default. 

                showExportToDocument
              
              
                It allows you to display or not to display the Document File element in the Save menu. The true value is set by default.  

                showExportToPdf
              
              
                It enables the display of the Adobe PDF File export menu item when viewing reports and the Adobe PDF when viewing dashboards. The property has the true value by default. 

                showExportToXps
              
              
                It enables the display of the XPS File export menu item. The property has the true value by default. 

                showExportToPowerPoint
              
              
                It enables the display of the Microsoft PowerPoint export menu item. The property has the true value by default. 

                showExportToHtml
              
              
                It allows you to display or not to display the HTML File element in the export settings menu. The true value is set by default. 

                showExportToHtml5
              
              
                It allows you to display or not to display the HTML5 File element in the export settings menu. The true value is set by default.   

                showExportToText
              
              
                It enables the display of the the Text File export menu item. The property has the true value by default.

                showExportToWord
              
              
                It enables the display of the the Microsoft Word export menu item. The property has the true value by default.

                showExportToOpenDocumentWriter
              
              
                It enables the display of the OpenDocument Writer File export menu item. The property has the true value by default. 

                showExportToExce
              
              
                It enables the display of the Microsoft Word export menu item. The property has the true value by default. 

                showExportToOpenDocumentCalc
              
              
                It enables the display of the OpenDocument Calc File export menu item. The property has the true value by default.  

                showExportToRtf
              
              
                It enables display of the RTF type in the settings of the Data export menu item. By default, the property is set to true.

                showExportToCsv
              
              
                It enables display of the CSV type in the settings of the Data export menu item. By default, the property is set to true.

                showExportToJson
              
              
                It enables display of the JSON type in the settings of the Data export menu item. By default, the property is set to true..  

                showExportToXml
              
              
                It enables display of the XML type in the settings of the Data export menu item. By default, the property is set to true.

                showExportToDbf
              
              
                It enables display of the DBF type in the settings of the Data export menu item. By default, the property is set to true.

                showExportToDif
              
              
                It enables display of the DIF type in the settings of the Data export menu item. By default, the property is set to true.

                showExportToSylk
              
              
                It enables display of the SYLK type in the settings of the Data export menu item. By default, the property is set to true.

                showExportToImagePng
              
              
                It enables display of the PNG type in the settings of the Image export menu item. By default, the property is set to true.

                showExportToImageJpeg
              
              
                It enables display of the JPEG type in the settings of the Image export menu item. By default, the property is set to true.

                showExportToImageSvg
              
              
                It enables display of the SVG type in the settings of the Image export menu item. By default, the property is set to true.

                showExportToImageSvgz
              
              
                It enables display of the SVGZ type in the settings of the Image export menu item. By default, the property is set to true.

                showExportToImagePcx
              
              
                It enables display of the PCX type in the settings of the Image export menu item. By default, the property is set to true.

                showExportToImageBmp
              
              
                It enables display of the BMP type in the settings of the Image export menu item. By default, the property is set to true.

                showExportToImageGif
              
              
                It enables display of the GIF type in the settings of the Image export menu item. By default, the property is set to true.

                showExportToImageTiff
              
              
                It enables display of the TIFF type in the settings of the Image export menu item. By default, the property is set to true.

                showExportDataOnly
              
              
                It enables display of the Export Data Only type in the settings of the Data export menu item. By default, the property is set to true.

          Email

                Name
              
              
                Description

                showEmailDialog
              
              
                It enables the display of the parameter dialog window of report sending by Email. If the dialog window is disabled, the sending by Email will be done with the settings specified by default onEmailReport. The true value is set by default.

                showExportDialog
              
              
                It enables the display of the parameter dialog window when sending an Email. If the property has the false value, the export will be done with specified by default settings. The true value is set by default. 

                defaultEmailAddress
              
              
                It sets an Email recipient by default, i.e. the address which will receive a Email with an attached report. The value is not set by default. 

                defaultEmailSubject
              
              
                It sets the theme (header) of an Email by default. The value is not set by default.

                defaultEmailMessage
              
              
                It sets a message (text) of an Email by default. The value is not set by default.**
