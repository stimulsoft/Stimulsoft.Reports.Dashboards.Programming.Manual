# Designer Settings

The HTML5 Designer is configured using properties that are located in the **Stimulsoft.Designer.StiDesignerOptions** class. All properties are split into groups. Some of the groups contain subgroups for ease of use. The following is an example of setting the properties of the viewer.


**designer.html**

```html
...
<script type="text/javascript">
    var report = new Stimulsoft.Report.StiReport();
    report.loadFile("SimpleList.mrt");
    
    var options = new Stimulsoft.Designer.StiDesignerOptions();
    options.appearance.theme = Stimulsoft.Designer.StiDesignerTheme.Office2022WhiteBlue;
    options.viewerOptions.appearance.reportDisplayMode = Stimulsoft.Report.Export.StiHtmlExportMode.Auto;
    options.toolbar.showFileMenuExit = false;
    options.toolbar.showFileMenuOptions = false;
    options.bands.showChildBand = false;
    options.components.showPanel = false;
    options.appearance.showReportTree = false;
    options.appearance.showTooltips = false;
    
    var designer = new Stimulsoft.Designer.StiDesigner(options);
    designer.report = report;
</script>
...
```

### Main settings (without groups)

| **Name** | **Description** |
| --- | --- |
| `Width` | Sets the width of the component in “px” or “%”. |
| `Height` | Sets the height of the component in “px” or “%”. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| `theme` | Specifies the theme of the designer layout. The list of available themes can be found in the `StiDesignerTheme` enumeration. The default value is `Office2022WhiteBlue`. |
| `defaultUnit` | Sets the units for the size of the report and all its components. - `Stimulsoft.Report.StiReportUnitType.Centimeters` (default value); - `Stimulsoft.Report.StiReportUnitType.HundredthsOfInch;` - `Stimulsoft.Report.StiReportUnitType.Inches;` - `Stimulsoft.Report.StiReportUnitType.Millimeters.` |
| `zoom` | Sets the zoom for displaying report pages. The default setting is 100 percent. It can take one of the following values of the `StiZoomMode` enumeration: - `PageWidth` – when the designer runs, the zoom, necessary to display the report by the page width, will be set; - `PageHeight` – when the designer runs, the zoom, required to display the page height of the report, will be set. |
| `interfaceType` | Sets the type of interface used for the designer. It can take one of the following values: - `Stimulsoft.Designer.StiInterfaceType.Auto` – the interface type of the designer will be selected automatically depending on the device used (default value); - `Stimulsoft.Designer.StiInterfaceType.Mouse` – forced use of the interface to control the designer with the mouse device; - `Stimulsoft.Designer.StiInterfaceType.Touch` – forced use of the touch interface to control the designer via the touch screen (mobile devices), also in this mode, the interface elements are increased. |
| `showAnimation` | Enables animation for various elements of the designer interface. By default, the property is set to `true`. |
| `showSaveDialog` | Enables displaying the dialog to insert a report name when it is saved. The name of the report will be transferred in the parameters of the report designer. By default, the property is set to `true`. |
| `showTooltips` | Enables displaying tooltips for designer controls when the mouse hovers over. By default, the property is set to `true`. |
| `showTooltipsHelp` | Enables displaying links to online documentation in tooltips for designer controls. By default, the property is set to `true`. |
| `showDialogsHelp` | Sets a value which indicates that show or hide the help button in dialogs. By default, the property is set to `true`. |
| `fullScreenMode` | Sets the full screen display mode of the designer. If the property is set to `true`, the values of the width and height properties are ignored. By default, the property is set to `false`. |
| `maximizeAfterCreating` | Sets a value which indicates that the designer will be maximized after creation. By default, the property is set to `false`. |
| `showLocalization` | Sets a visibility of the localization control of the designer. By default, the property is set to `true`. |
| `allowChangeWindowTitle` | Allows using a title of the browser window to display the file name of the edited report. By default, the property is set to `true`. |
| `showPropertiesGrid` | Enables displaying the Property panel of the report designer. By default, the property is set to `true`. |
| `showReportTree` | Enables displaying the tree of report components. By default, the property is set to `true`. |
| `propertiesGridPosition` | Sets **Left** or **Right** position of the properties grid in the designer. |
| `showSystemFonts` | Sets a visibility of the system fonts in the fonts list. By default, the property is set to `true`. |
| `datePickerFirstDayOfWeek` | Sets the first day of week in the date picker. - `Stimulsoft.Designer.StiFirstDayOfWeek.Auto` - Sets **Monday** or **Sunday** as the first day depending on the browser culture (default value); - `Stimulsoft.Designer.StiFirstDayOfWeek.Monday` - Sets **Monday** as the first day of the week. - `Stimulsoft.Designer.StiFirstDayOfWeek.Sunday` - Sets **Sunday** as the first day of the week. |
| `formatForDateControls` | This feature allows you to customize the format for date controls. By default, the current option does not have a specified value, and the date format is determined based on the browser's locale. |
| `wizardTypeRunningAfterLoad` | Calls the Report wizard after starting the report designer. It may have one of the following `StiWizardType` enumeration values: - `None` - runs the report designer without running the report wizard (default value); - `StandardReport` - runs the Standard wizard; - `MasterDetailReport` - runs the Master-Detail wizard; - `LabelReport` - runs the Label wizard; - `InvoicesReport` - runs the Invoice wizard; - `OrdersReport` - runs the Order wizard; - `QuotationReport` - runs the Quote wizard. |
| `defaultRibbonType` | Allows setting the default style for the designer's toolbar. It can take one of the following values from the enumeration: - `StiDesignerRibbonType.Classic` - the classic style will be set (default value); - `StiDesignerRibbonType.SingleLine` – a compact single-line style will be set. |
| `allowPropagationEvents` | Allows the propagation of key press events when the report designer is not in focus. By default, the property is set to `true`. |
| `propertiesPanelViewMode` | Provides the ability to pin or unpin the Properties panel, Report Dictionary, and Report Tree. It can take one of the following values from the enumeration: - `Pinned` — panels are pinned (default value); - `Unpinned` — panels are unpinned. |


### Toolbar

| **Name** | **Description** |
| --- | --- |
| `visible` | It enables the display of toolbar in the report designer. The property has the `true` value by default. |
| `showPreviewButton` | It enables or disables the display of the **Preview** button in the designer toolbar. The property has the `true` value by default. |
| `showSaveButton` | It enables the display of the **Save** button in the designer toolbar. The property has the `true` value by default. |
| `showAboutButton` | It enables the display of the **About** button in the designer toolbar. The property has the `false` value by default. |
| `showFileMenu` | It enables the display of the main menu of the report designer. The property has the `true` value by default. |
| `showFileMenuNew` | It enables the display of the **New** main menu item.  The property has the `true` value by default. |
| `showFileMenuOpen` | It enables the display of the **Open** main menu item. The property has the `true` value by default. |
| `showFileMenuSave` | It enables the display of the **Save** main menu item. The property has the `true` value by default. |
| `showFileMenuSaveAs` | It enables the display of the **Save as** main menu item. The property has the `true` value by default. |
| `showFileMenuClose` | It enables the display of the **Close** main menu item. The property has the `true` value by default. |
| `showFileMenuExit` | It enables the display of the **Exit** main menu item. The property has the `false` value by default. |
| `showFileMenuReportSetup` | It enables the display of the **Report Setup** main menu item. The property has the `true` value by default. |
| `showFileMenuOptions` | It enables the display of the **Options** main menu item. The property has the `true` value by default. |
| `showFileMenuInfo` | It enables the display of the **Info** main menu item.  The property has the `true` value by default. |
| `showFileMenuAbout` | It enables the display of the **About** main menu item.  The property has the `true` value by default. |
| `showFileMenuNewReport` | It enables or disables the display of the **New Page** main menu item. The property has the `true` value by default. |
| `showFileMenuNewDashboard` | It enables or disables the display of the **New Dashboard** main menu item. The property has the `true` value by default. |
| `showSetupToolboxButton` | It enables or disables the display of the report components side panel settings invoke button. The property has the `true` value by default. |
| `showNewPageButton` | It enables or disables the display of the **New Page** button in the toolbar. The property has the `true` value by default. |
| `showNewDashboardButton` | It enables or disables the display of the **New Dashboard** button in the toolbar. The property has the `true` value by default. |


### Bands

| **Name** | **Description** |
| --- | --- |
| `showReportTitleBand` | It enables the display of the **Report Title** band in the designer components insert menu. The property has the `true` value by default. |
| `showReportSummaryBand` | It enables the display of the **Report Summary** band in the designer components insert menu. The property has the `true` value by default. |
| `showPageHeaderBand` | It enables the display of the **Page Header** band in the designer components insert menu. The property has the `true` value by default. |
| `showPageFooterBand` | It enables the display of the **Page Footer** band in the designer components insert menu. The property has the `true` value by default. |
| `showGroupHeaderBand` | It enables the display of the **Group Header** band in the designer components insert menu. The property has the `true` value by default. |
| `showGroupFooterBand` | It enables the display of the **Group Footer** band in the designer components insert menu. The property has the `true` value by default. |
| `showHeaderBand` | It enables the display of the **Header** band in the designer components insert menu. The property has the `true` value by default. |
| `showFooterBand` | It enables the display of the **Footer** band in the designer components insert menu. The property has the `true` value by default. |
| `showColumnHeaderBand` | It enables the display of the **Column Header** band in the designer components insert menu. The property has the `true` value by default. |
| `showColumnFooterBand` | It enables the display of the **Column Footer** band in the designer components insert menu. The property has the `true` value by default. |
| `showDataBand` | It enables the display of the **Data** band in the designer components insert menu. The property has the `true` value by default. |
| `showHierarchicalBand` | It enables the display of the **Hierarchical** band in the designer components insert menu. The property has the `true` value by default. |
| `showChildBand` | It enables the display of the **Child** band in the designer components insert menu. The property has the `true` value by default. |
| `showEmptyBand` | It enables the display of the **Empty** band in the designer components insert menu. The property has the `true` value by default. |
| `showOverlayBand` | It enables the display of the **Overlay** band in the designer components insert menu. The property has the `true` value by default. |
| `showTable` | It enables the display of the **Table** component in the designer components insert menu. The property has the `true` value by default. |
| `showTableOfContents` | It enables the display of the **Table of Contents** band in the designer components insert menu. The property has the `true` value by default. |


### Cross-Bands

| **Name** | **Description** |
| --- | --- |
| `showCrossTab` | It enables the display of the **Cross-Tab** component in the designer components insert menu. The property has the `true` value by default. |
| `showCrossGroupHeaderBand` | It enables the display of the **Cross-Group Header** band in the designer components insert menu. The property has the `true` value by default. |
| `showCrossGroupFooterBand` | It enables the display of the **Cross-Group Footer** band in the designer components insert menu. The property has the `true` value by default. |
| `showCrossHeaderBand` | It enables the display of the **Cross-Header** band in the designer components insert menu. The property has the `true` value by default. |
| `showCrossFooterBand` | It enables the display of the **Cross-Footer** band in the designer components insert menu. The property has the `true` value by default. |
| `showCrossDataBand` | It enables the display of the **Cross-Data** band in the designer components insert menu. The property has the `true` value by default. |


### dashboardElements

**Name
              
              
                Description

                showTableElement
              
              
                It enables the display of the Table dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showCardsElement
              
              
                It enables the display of the Cards dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showChartElement
              
              
                It enables the display of the Chart dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showGaugeElement
              
              
                It enables the display of the Gauge dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showPivotTableElement
              
              
                It enables the display of the Pivot dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showIndicatorElement
              
              
                It enables the display of the Indicator dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showProgressElement
              
              
                It enables the display of the Progress dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showRegionMapElement
              
              
                It enables the display of the Region Map dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showOnlineMapElement
              
              
                It enables the display of the Online Map dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showImageElement
              
              
                It enables the display of the Image dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showTextElement
              
              
                It enables the display of the Text dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showPanelElement
              
              
                It enables the display of the Panel dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showShapeElement
              
              
                It enables the display of the Shape dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showButtonElement
              
              
                It enables the display of the Button dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showListBoxElement
              
              
                It enables the display of the List Box dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showComboBoxElement
              
              
                It enables the display of the Combo Box dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showTreeViewElement
              
              
                It enables the display of the Tree View dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showTreeViewBoxElement
              
              
                It enables the display of the Tree View Box dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.

                showDatePickerElement
              
              
                It enables the display of the Date Picker dashboard element in the toolbox or the Insert tab in the designer. The property has the true value by default.**


### Components

| **Name** | **Description** |
| --- | --- |
| `showText` | It enables the display of the **Text** component in the designer components insert menu. The property has the `true` value by default. |
| `showTextInCells` | It enables the display of the **Text in Cells** component in the designer components insert menu. The property has the `true` value by default. |
| `showRichText` | It enables the display of the **Rich** **Text** component in the designer components insert menu. The property has the `true` value by default. |
| `showImage` | It enables the display of the **Image** component in the designer components insert menu. The property has the `true` value by default. |
| `showBarCode` | It enables the display of the **Bar Code** component in the designer components insert menu. The property has the `true` value by default. |
| `showShape` | It enables the display of the **Shape** component in the designer components insert menu. The property has the `true` value by default. |
| `showPanel` | It enables the display of the **Panel** component in the designer components insert menu. The property has the `true` value by default. |
| `showClone` | It enables the display of the **Clone** component in the designer components insert menu. The property has the `true` value by default. |
| `showCheckBox` | It enables the display of the **Check Box** component in the designer components insert menu. The property has the `true` value by default. |
| `showSubReport` | It enables the display of the **Text** component in the designer components insert menu. The property has the `true` value by default. |
| `showZipCode` | It enables the display of the **Sub-Report** component in the designer components insert menu. The property has the `true` value by default. |
| `showChart` | It enables the display of the **Chart** component in the designer components insert menu. The property has the `true` value by default. |
| `showGauge` | It enables the display of the **Gauge** component in the designer components insert menu. The property has the `true` value by default. |
| `showSparkline` | It enables the display of the **Sparkline** component in the designer components insert menu. The property has the `true` value by default. |
| `showMathFormula` | It enables the display of the **Math Formula** component in the designer components insert menu. The property has the `true` value by default. |
| `showMap` | It enables the display of the **Map** component in the designer components insert menu. The property has the `true` value by default. |


### Dictionary

| **Name** | **Description** |
| --- | --- |
| `showAdaptersInNewConnectionForm` | It enables the display of the **Object** category in the new connection creation window. The property has the `true` value by default. |
| `showDictionary` | It enables the display of the report dictionary. The property has the `true` value by default. |
| `newReportDictionary` | It allows you to create a new data dictionary or join the existing one when creating a new report in the designer. It can take one of the specified below enumeration values: - `StiNewReportDictionary.Auto` - defines the mode to create or join the data dictionary from a saved value in cookies (default value); - `StiNewReportDictionary.DictionaryNew` - sets the mode to create a new data dictionary when creating a new report; - `StiNewReportDictionary.DictionaryMerge` - sets the mode to join the existing data dictionary with a new one when creating a new report in the designer. |
| `useAliases` | Allows you to use aliases in the data dictionary. It can take one of the specified below enumeration values: - `StiUseAliases.Auto` - defines the mode of using aliases from a saved value in cookies (default value); - `StiUseAliases.True` - sets the mode of using aliases in the data dictionary; - `StiUseAliases.False` - disables the mode of using aliases in the data dictionary. |
| `showDictionaryContextMenuProperties` | Sets a visibility of the **Properties** item in the dictionary context menu. By default, the property is set to `true`. |
| `showDictionaryActions` | Sets a visibility of the **Actions** **menu** on the dictionary toolbar. By default, the property is set to **true**. |
| `dataSourcesPermissions` | It sets available actions on report data sources. It can take one or several values from the `StiDesignerPermissions` enumeration. |
| `dataConnectionsPermissions` | It sets available actions on connections to report data. It can take one or several values from the `StiDesignerPermissions` enumeration. |
| `dataColumnsPermissions` | It sets available actions on report data columns. It can take one or several values from the `StiDesignerPermissions` enumeration. |
| `dataRelationsPermissions` | It sets available actions on report data connections. It can take one or several values from the `StiDesignerPermissions` enumeration. |
| `businessObjectsPermissions` | It sets available actions on report business objects. It can take one or several values from the `StiDesignerPermissions` enumeration. |
| `variablesPermissions` | It sets available actions on report variables. It can take one or several values from the `StiDesignerPermissions` enumeration. |
| `resourcesPermissions` | It sets available actions on sources in report dictionary. It can take one or several values from the `StiDesignerPermissions` enumeration. |
| `dataTransformations` | Sets the available actions on data transformation. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `userFunctions` | Sets the available actions for the user functions. It can take one or more values from the `StiDesignerPermissions` enumeration. |

In the table below you can see all available values for the `StiDesignerPermissions` enumeration. They can be set for report dictionary elements.


| **Name** | **Description** |
| --- | --- |
| `None` | Disables any action on the item of the data dictionary. |
| `Create` | It allows you to create definite element of the dictionary. |
| `Delete` | It allows you to delete a definite element of the dictionary. |
| `Modify` | It allows you to edit a definite element of the dictionary. |
| `View` | It allows you to view a definite element of the dictionary. |
| `ModifyView` | It allows you to edit and view a definite element of the dictionary. |
| `All` | It allows you to make any actions on the dictionary element. |

You can configure the built-in `StiViewer` component used to preview the report. To get access to all of its settings, you should use the `viewerOptions` property, which is an object of the viewer options. All its properties are described in the [Viewer settings](../Web_Viewer/Settings.md) section.
