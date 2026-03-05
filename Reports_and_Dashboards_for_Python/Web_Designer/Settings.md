# Designer Settings

The designer is configured by modifying the property values located in the main properties container called `options` of the component. All properties are divided into groups for ease of use. All enumerations used in the viewer settings are located in the namespace `stimulsoft_reports.designer.enums`.


An example of modifying some designer settings:


**app.py**

```python

from flask import Flask, request
from stimulsoft_reports.designer import StiDesigner
from stimulsoft_reports.designer.enums import StiReportUnitType, StiDesignerTheme

@app.route('/designer', methods = ['GET', 'POST'])
def designer():
    designer = StiDesigner()
    designer.options.appearance.theme = StiDesignerTheme.OFFICE_2022_DARKGRAY_BLUE
    designer.options.appearance.defaultUnit = StiReportUnitType.CENTIMETERS
    designer.options.appearance.showReportTree = False
    designer.options.appearance.showTooltips = False
    designer.options.bands.showChildBand = False
    designer.options.components.showPanel = False
    designer.options.toolbar.showFileMenuExit = False
    designer.options.toolbar.showFileMenuOptions = False

    if designer.processRequest(request):
        return designer.getFrameworkResponse()

    # Here is the code for working with the report

    return designer.getFrameworkResponse()
```

### Main (without group)

| **Name** | **Description** |
| --- | --- |
| `width` | Sets the width of the component in "px" or "%". By default, the value is set to "100%". |
| `height` | Sets the height of the component in "px" or "%". By default, the value is set to "100%" for standard mode and "650px" for scroll mode. |
| `localization` | Sets the selected localization of the component. By default, the English localization is embedded in the component. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| `theme` | Sets the [theme of the designer](../../Reports_and_Dashboards_for_PHP/Web_Designer/Using_Themes.md). The list of available themes is in the  `StiDesignerTheme`. By default, the value is set to `StiDesignerTheme.OFFICE_2022_WHITE_BLUE`. |
| `iconSet` | Allows setting the icon set: - `StiWebUIIconSet.AUTO` (default value) -automatically sets the icon set. For `Office2022` themes, a `Monoline` icon set is used, and for `Office2013` themes, a `Regular` icon set is used. - `StiWebUIIconSet.MONOLINE` - sets the `Monoline` icon set; - `StiWebUIIconSet.REGULAR` - sets the `Regular` icon set. |
| `defaultUnit` | Sets the background color of the viewer. By default, the value is `'white'`. - `StiReportUnitType.CENTIMETERS`(default value); - `StiReportUnitType.HUNDREDTHS_OF_INCH`**;** - `StiReportUnitType.INCHES`**;** - `StiReportUnitType.MILLIMETERS`**.** |
| `zoom` | Sets the scale for displaying report pages. The default scale is set to 100 percent. Allowed values range from 10 to 200 percent. It can take one of the following values from the `StiZoomMode` enumeration: - `StiZoomMode.PAGE_WIDTH` – scales the report pages to the width of the page; - `StiZoomMode.PAGE_HEIGHT` – scales the report pages to the height of the page. |
| `interfaceType` | Sets the interface type of the designer . The following values can be used: - `StiInterfaceType.AUTO` – the designer interface type will be automatically selected based on the device being used (default value); - `StiInterfaceType.MOUSE` – forces the use of the standard interface for controlling the viewer with a mouse; - `StiInterfaceType.TOUCH` – forces the use of the Touch interface for controlling the viewer with a touchscreen monitor; in this mode, the viewer’s interface elements are larger for ease of use; |
| `showAnimation` | Enables or disables animation for displaying and closing various menus in the viewer. By default, this is set to `True`. |
| `showSaveDialog` | Enables the display of the report name input dialog when saving a report. The report name will be passed in the designer parameters. By default, the property is set to `True`. |
| `showTooltips` | Enables the display of tooltips when hovering over the viewer’s tools. By default, the value is set to `True`. |
| `showTooltipsHelp` | Allows displaying a link to the documentation in the tooltips when hovering over the viewer’s tools. By default, the value is set to `True`. |
| `showDialogsHelp` | Allows displaying or hiding the help button in various menus. By default, the value is set to `True`. |
| `fullScreenMode` | Sets the full-screen mode for the designer. If this property is set to True, the width and height properties are ignored. By default, the value is set to `False`. |
| `maximizeAfterCreating` | Allows setting the maximum size of the report designer. By default, the property is set to `False`. |
| `showLocalization` | Provides the option to show or hide the localization control in the report designer. By default, the property is set to `True`. |
| `allowChangeWindowTitle` | Allows the use of the browser window title to display the name of the edited report file. By default, the property is set to `True`. |
| `showPropertiesGrid` | Enables the display of the properties panel in the report designer. By default, the property is set to `True`. |
| `showReportTree` | Enables the display of the report components tree. By default, the property is set to `True`. |
| `propertiesGridPosition` | Provides the option to define the position of the properties panel. The following values can be used: - `StiPropertiesGridPosition.LEFT` – the properties panel will be displayed on the left (default value); - `StiPropertiesGridPosition.RIGHT`  – the properties panel will be displayed on the right. |
| `showSystemFonts` | Provides the option to show or hide system fonts in the font list. By default, the property is set to True, meaning system fonts are displayed in the font list. |
| `datePickerFirstDayOfWeek` | Allows setting the first day of the week for the **Date Picker** tool. - `StiFirstDayOfWeek.AUTO` - Monday or Sunday will be set as the first day of the week based on the browser culture; - `StiFirstDayOfWeek.MONDAY` - Monday will be set as the first day of the week; - `StiFirstDayOfWeek.SUNDAY` - Sunday will be set as the first day of the week.Sunday will be set as the first day of the week. |
| `formatForDateControls` | This feature allows you to customize the format for date controls. By default, the current option doesn't have a specified value, and the date format is determined based on the browser's locale. |
| `undoMaxLevel` | Sets the maximum undo depth for changes to the report while editing. This affects memory consumption. By default, it is set to 6 changes. |
| `wizardTypeRunningAfterLoad` | Provides the option to call the report creation wizard after starting the report designer. It can take one of the following values from the enumeration: - `StiWizardType.NONE` - the report designer will start without calling the report creation wizard (default value); - `StiWizardType.STANDARD_REPORT` - the report designer will start with the standard report creation wizard; - `StiWizardType.MASTER_DETAIL_REPORT` - the report designer will start with the master-detail report creation wizard; - `StiWizardType.LABEL_REPORT` - the report designer will start with the label report creation wizard; - `StiWizardType.INVOICES_REPORT` - the report designer will start with the invoice creation wizard; - `StiWizardType.ORDERS_REPORT` - the report designer will start with the order creation wizard; - `StiWizardType.QUOTATION_REPORT` - the report designer will start with the quotation creation wizard. |
| `allowWordWrapTextEditors` | Enables or disables line wrapping in text editors in the designer. By default, the property is set to `True`. |
| `defaultRibbonType` | Allows setting the default style for the designer's toolbar. It can take one of the following values from the enumeration: - `StiDesignerRibbonType.CLASSIC` - the classic style will be set (default value); - `StiDesignerRibbonType.SINGLE_LINE` – a compact single-line style will be set. |
| `allowPropagationEvents` | Allows the propagation of key press events when the report designer is not in focus. By default, the property is set to `true`. |
| `propertiesPanelViewMode` | Provides the ability to pin or unpin the Properties panel, Report Dictionary, and Report Tree. It can take one of the following values from the enumeration: - `Pinned` — panels are pinned (default value); - `Unpinned` — panels are unpinned. |


### Toolbar

| **Name** | **Description** |
| --- | --- |
| `visible` | Enables the display of the toolbar in the report designer. By default, the property is set to `True`. |
| `showPreviewButton` | Enables or disables the display of the **Preview** button on the designer toolbar. By default, the property is set to `True`. |
| `showSaveButton` | Enables the display of the **Save** button on the designer's toolbar. By default, this is set to `False`. |
| `showAboutButton` | Enables the display of the **About** button on the designer toolbar. By default, the property is set to `False`. |
| `showFileMenu` | Enables the display of the main menu in the report designer. By default, the property is set to `True`. |
| `showFileMenuNew` | Enables the display of the **New** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuOpen` | Enables the display of the **Open** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuSave` | Enables the display of the Save item in the main menu. By default, the property is set to `True`. |
| `showFileMenuSaveAs` | Enables the display of the **Save As** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuClose` | Enables the display of the **Close** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuExit` | Enables the display of the **Exit** item in the main menu. By default, the property is set to `False`. |
| `showFileMenuReportSetup` | Enables the display of the **Report Setup** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuOptions` | Enables the display of the **Options** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuInfo` | Enables the display of the **Info** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuAbout` | Enables the display of the **About** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuNewReport` | Enables or disables the display of the **New Page** item in the main menu. By default, the property is set to `True`. |
| `showFileMenuNewDashboard` | Enables or disables the display of the **New Dashboard** item in the main menu. By default, the property is set to `True`. |
| `showSetupToolboxButton` | Enables or disables the display of the settings button for the report component sidebar. By default, the property is set to `True`. |
| `showNewPageButton` | Enables or disables the display of the **New Page** button on the toolbar. By default, the property is set to `True`. |
| `showNewDashboardButton` | Enables or disables the display of the **New Dashboard** button on the toolbar. By default, the property is set to `True`. |


### Bands

| **Name** | **Description** |
| --- | --- |
| `showReportTitleBand` | Enables the display of the **Report Title** section in the **Sections** menu. By default, the property is set to `True`. |
| `showReportSummaryBand` | Enables the display of the **Report Summary** section in the **Sections** menu. By default, the property is set to `True`. |
| `showPageHeaderBand` | Enables the display of the **Page Header** section in the **Sections** menu. By default, the property is set to `True`. |
| `showPageFooterBand` | Enables the display of the **Page Footer** section in the **Sections** menu. By default, the property is set to `True`. |
| `showGroupHeaderBand` | Enables the display of the **Group Header** section in the **Sections** menu. By default, the property is set to `True`. |
| `showGroupFooterBand` | Enables the display of the **Group Footer** section in the **Sections** menu. By default, the property is set to `True`. |
| `showHeaderBand` | Enables the display of the **Header** section in the **Sections** menu. By default, the property is set to `True`. |
| `showFooterBand` | Enables the display of the **Footer** section in the **Sections** menu. By default, the property is set to `True`. |
| `showColumnHeaderBand` | Enables the display of the **Column Header** section in the **Sections** menu. By default, the property is set to `True`. |
| `showColumnFooterBand` | Enables the display of the **Column Footer** section in the **Sections** menu. By default, the property is set to `True`. |
| `showDataBand` | Enables the display of the **Data** section in the **Sections** menu. By default, the property is set to `True`. |
| `showHierarchicalBand` | Enables the display of the **Hierarchical** section in the **Sections** menu. By default, the property is set to `True`. |
| `showChildBand` | Enables the display of the **Child** section in the **Sections** menu. By default, the property is set to `True`. |
| `showEmptyBand` | Enables the display of the **Empty** section in the **Sections** menu. By default, the property is set to `True`. |
| `showOverlayBand` | Enables the display of the **Overlay** section in the **Sections** menu. By default, the property is set to `True`. |
| `showTable` | Enables the display of the **Table** component in the **Sections** menu. By default, the property is set to `True`. |
| `showTableOfContents` | Enables or disables the display of the **Table of Contents** component in the **Sections** menu. By default, the property is set to `True`. |


### Cross-Bands

| **Name** | **Description** |
| --- | --- |
| `showCrossTab` | Enables the display of the **Cross-Tab** component in the Cross menu. By default, the property is set to `True`. |
| `showCrossGroupHeaderBand` | Enables the display of the **Cross Group Header** section in the Cross menu. By default, the property is set to `True`. |
| `showCrossGroupFooterBand` | Enables the display of the **Cross Group Footer** section in the Cross menu. By default, the property is set to `True`. |
| `showCrossHeaderBand` | Enables the display of the **Cross Header** section in the Cross menu. By default, the property is set to `True`. |
| `showCrossFooterBand` | Enables the display of the **Cross Footer** section in the Cross menu. By default, the property is set to `True`. |
| `showCrossDataBand` | Enables the display of the **Cross Data** section in the Cross menu. By default, the property is set to `True`. |


### Dashboard Elements

**Name
              
              
                Description

                showTableElement
              
              
                Enables the display of the Table indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showCardsElement
              
              
                Enables the display of the Cards indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showChartElement
              
              
                Enables the display of the Chart indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showGaugeElement
              
              
                Enables the display of the Gauge indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showPivotTableElement
              
              
                Enables the display of the Pivot Table indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showIndicatorElement
              
              
                Enables the display of the Indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showProgressElement
              
              
                Enables the display of the Progress panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showRegionMapElement
              
              
                Enables the display of the Region Map panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showOnlineMapElement
              
              
                Enables the display of the Online Map panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showImageElement
              
              
                Enables the display of the Image panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showTextElement
              
              
                Enables the display of the Text panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showPanelElement
              
              
                Enables the display of the Panel panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showShapeElement
              
              
                Enables the display of the Shape panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showButtonElement
              
              
                Enables the display of the Button panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showListBoxElement
              
              
                Enables the display of the ListBox panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showComboBoxElement
              
              
                Enables the display of the ComboBox panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showTreeViewElement
              
              
                Enables the display of the Tree View panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showTreeViewBoxElement
              
              
                Enables the display of the Tree ViewBox indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.

                showDatePickerElement
              
              
                nables the display of the Date Picker indicator panel item in the toolbar or the Insert tab in the designer. By default, the property is set to True.**


### Components

| **Name** | **Description** |
| --- | --- |
| `showText` | Enables the display of the **Text** component in the **Components** menu. By default, the property is set to `True`. |
| `showTextInCells` | Enables the display of the **Text** in Cells component in the **Components** menu. By default, the property is set to `True`. |
| `showRichText` | Enables the display of the **Rich** Text component in the **Components** menu. By default, the property is set to `False`. |
| `showImage` | Enables the display of the **Image** component in the **Components** menu. By default, the property is set to `True`. |
| `showBarCode` | Enables the display of the **Bar Code** component in the toolbar or the Insert tab in the designer. By default, the property is set to `True`. |
| `showShape` | Enables the display of the **Shape** component in the toolbar or the Insert tab in the designer. By default, the property is set to `True`. |
| `showPanel` | Enables the display of the **Panel** component in the **Components** menu. By default, the property is set to `True`. |
| `showClone` | Enables the display of the **Clone** component in the **Components** menu. By default, the property is set to `False`. |
| `showCheckBox` | Enables the display of the **Check Box** component in the **Components** menu. By default, the property is set to `True`. |
| `showSubReport` | Enables the display of the **Sub Report** component in the **Components** menu. By default, the property is set to `True`. |
| `showZipCode` | Enables the display of the **Zip Code** component in the **Components** menu. By default, the property is set to `False`. |
| `showChart` | Enables the display of the **Chart** component in the toolbar or the Insert tab in the designer. This applies to all chart types. By default, the property is set to `True`. |
| `showGauge` | Enables or disables the display of the **Gauge** component in the toolbar or the Insert tab in the designer. By default, the property is set to `True`. |
| `showSparkline` | Enables the display of the **Sparkline** component in the **Components** menu. By default, the property is set to `True`. |
| `showMathFormula` | Enables or disables the display of the **Math Formula** component in the **Components** menu. By default, the property is set to `False`. |
| `showMap` | Enables or disables the display of the **Map** component in the toolbar or the Insert tab in the designer. By default, the property is set to `True`. |


### Dictionary

| **Name** | **Description** |
| --- | --- |
| `showAdaptersInNewConnectionForm` | Enables the display of the **Object** category in the new connection window. By default, the property is set to `True`. |
| `showDictionary` | Enables the display of the report's data dictionary. By default, the property is set to `True`. |
| `newReportDictionary` | Allows the creation of a new data dictionary or merging it with an existing one when creating a new report in the designer. It can take one of the following values: - `StiNewReportDictionary.AUTO` - determines the mode of creating or merging the data dictionary from the saved value in `cookies` (default value); - `StiNewReportDictionary.DICTIONARY_NEW` - sets the mode to create a new data dictionary when creating a new report; - `StiNewReportDictionary.DICTIONARY_MERGE` - sets the mode to merge an existing data dictionary with the new one when creating a new report in the designer. |
| `useAliases` | Allows the use of aliases in the data dictionary. It can take one of the specified values: - `StiUseAliases.AUTO` - determines the mode for using aliases from the saved value in `cookies` (default value); - `StiUseAliases.True` - enables the use of aliases in the data dictionary; - `StiUseAliases.False` - disables the use of aliases in the data dictionary. |
| `showDictionaryContextMenuProperties` | Sets the visibility of the **Properties** item in the context menu of the data dictionary. By default, the property is set to `True`. |
| `showDictionaryActions` | Sets the display of the **Actions** menu on the data dictionary toolbar. By default, the property is set to `True`. |
| `dataSourcesPermissions` | Sets the available actions for data sources in the report. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `dataConnectionsPermissions` | Sets the available actions for data connections in the report. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `dataColumnsPermissions` | Sets the available actions for data columns in the report. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `dataRelationsPermissions` | Sets the available actions for data relationships in the report. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `businessObjectsPermissions` | Sets the available actions for business objects in the report. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `variablesPermissions` | Sets the available actions for report variables. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `resourcesPermissions` | Sets the available actions for resources in the report's data dictionary. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `dataTransformations` | Sets the available actions for data transformations. It can take one or more values from the `StiDesignerPermissions` enumeration. |
| `userFunctions` | Sets the available actions for the user functions. It can take one or more values from the `StiDesignerPermissions` enumeration. |

The table below lists all available values for the `StiDesignerPermissions` enumeration, which can be set for report dictionary elements.


| **Value** | **Description** |
| --- | --- |
| `StiDesignerPermissions.NONE` | Prohibits any action on a data dictionary element. |
| `StiDesignerPermissions.CREATE` | Allows creating a specific data dictionary element. |
| `StiDesignerPermissions.DELETE` | Allows deleting a specific data dictionary element. |
| `StiDesignerPermissions.MODIFY` | Allows editing a specific data dictionary element. |
| `StiDesignerPermissions.VIEW` | Allows viewing a specific data dictionary element. |
| `StiDesignerPermissions.MODIFY_VIEW` | Allows editing and viewing a specific data dictionary element. |
| `StiDesignerPermissions.ALL` | Allows any actions on a data dictionary element (default setting for all properties using this enumeration). |

The built-in `StiViewer` component is designed for report preview customization. To access all its settings, use the `viewerOptions` property, which represents a viewer options object. All its properties are described in the [Viewer Settings](../../Reports_and_Dashboards_for_PHP/Settings.md) section. For example, you may need to change the report display mode and disable unnecessary export formats:


**app.py**

```python

from flask import Flask, request
from stimulsoft_reports.designer import StiDesigner
from stimulsoft_reports.designer.enums import StiReportUnitType, StiDesignerTheme

@app.route('/designer', methods = ['GET', 'POST'])
def designer():
    designer = StiDesigner()
    designer.options.viewerOptions.exports.showExportToWord2007 = False
    designer.options.viewerOptions.exports.showExportToCsv = False

    if designer.processRequest(request):
        return designer.getFrameworkResponse()

    # Here is the code for working with the report

    return designer.getFrameworkResponse()
```
