# Designer Settings

The designer is set using the properties found in the `Stimulsoft.Designer.StiDesignerOptions` class. All properties are divided into groups for comfortable using. All designer classes and enums you may find in the `\Stimulsoft\Designer` namespace. To set the designer you should create the class of options, set required properties and transfer an object of options to the designer constructor as the first argument.


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner;
    use Stimulsoft\Designer\Enums\StiDesignerTheme;
    
    $designer = new StiDesigner();
    $designer->options->appearance->theme = StiDesignerTheme::Office2022WhiteGreen;
    $designer->options->toolbar->showFileMenuExit = false;
    $designer->options->toolbar->showFileMenuOptions = false;
    $designer->options->bands->showChildBand = false;
    $designer->options->components->showPanel = false;
    $designer->options->appearance->showReportTree = false;
    $designer->options->appearance->showTooltips = false;
?>
```

### Main settings (without groups)

| **Name** | **Description** |
| --- | --- |
| `Width` | It sets component width in "px or "%". The 100 % value is set by default. |
| `Height` | It sets component height in "px" or "%". The "800px" value is set by default. |
| `localization` | Sets the selected localization of the component. By default, the English localization is set. It is built into the component. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| `theme` | Sets the [theme of the designer](../../Reports_and_Dashboards_for_Python/Web_Designer/Using_Themes.md). The list of available themes can be found in the `StiDesignerTheme` enumeration. The default value is `Office2022WhiteBlue`. |
| `iconSet` | Allows setting the icon set: - `StiWebUIIconSet::Auto` (default) – automatically selects the icon set. For `Office2022` themes, the `Monoline` icon set is used, and for `Office2013` themes, the `Regular` icon set is used; - `StiWebUIIconSet::Monoline` - sets the `Monoline` icon set; - `StiWebUIIconSet::Regular` - sets the `Regular` icon set. |
| `defaultUnit` | It sets the units of measure of sizes for a report and all its components: - `StiReportUnitType::Centimeters` (value is set by default); - `StiReportUnitType::HundredthsOfInch`**;** - `StiReportUnitType::Inches`**;** - `StiReportUnitType::Millimeters`**.** |
| `zoom` | Sets the zoom for displaying report pages. The default setting is 100 percent. Values between 10% and 200% are allowed. It can take one of the following values of the `StiZoomMode` enumeration: - `StiZoomMode::PageWidth` – when the designer runs, the zoom, necessary to display the report by the page width, will be set; - `StiZoomMode::PageHeight` – when the designer runs, the zoom, required to display the page height of the report, will be set. |
| `interfaceType` | It sets the type of the designer interface. The following values can be used: - `StiInterfaceType::Auto` – the type of the designer interface will be selected automatically depending on the device you use (the value by default); - `StiInterfaceType::Mouse` – the forced using Mouse interface for controlling the designer using a computer mouse; - `StiInterfaceType::Touch` – the forced using of the Touch interface to control the designer using touch screen of a monitor. In this mode, the designer interface elements have enlarged sizes for comfortable control. |
| `showAnimation` | It allows you to enable or disable the animation of display and closing various menus in the designer. The `true` value is set by default. |
| `showSaveDialog` | It enables the display of the input dialog of report name when its saving. Report name will be transferred in the designer parameters. The `true` value is set by default. |
| `showTooltips` | It enables the display of prompts for the designer controls when hovering. The `true` value is set by default. |
| `showTooltipsHelp` | It enables the display of the link to the online documentation in prompts for the designer controls. The `true` value is set by default. |
| `showDialogsHelp` | It allows you to display or not to display the reference invoke button in various menus. The `true` value is set by default. |
| `fullScreenMode` | It sets the full screen mode of the designer display. If the property is set in the `true` value, the values of the width and height properties are ignored. The `false` value is set by default. |
| `maximizeAfterCreating` | It allows you to set max size of the report designer. The `false` value is set by default. |
| `showLocalization` | It allows you to display or not to display the localization control in the report designer. The `true` value is set by default. |
| `allowChangeWindowTitle` | It allows you to use the header of browser window to display file name of edited report.  The `true` value is set by default. |
| `showPropertiesGrid` | It enables the display of the property panel in the report designer. The `true` value is set by default. |
| `showReportTree` | It enables the display of report components tree. The `true` value is set by default. |
| `propertiesGridPosition` | It allows you to define the position of the property panel to the left or to the right: - `StiPropertiesGridPosition::Left` – the property panel will be displayed on the left (value is set by default); - `StiPropertiesGridPosition::Right`  – the property panel will be displayed on the right. |
| `showSystemFonts` | It allows you to display or not to display system fonts in the list of fonts. The property has the `true` value by default, i.e. system fonts are displayed in the list of fonts. |
| `datePickerFirstDayOfWeek` | It allows you to set the first day of the week for the **Date picker** element: - `StiFirstDayOfWeek::Auto` - Monday or Sunday will be set as the first day of the week depending on browser culture (value is set by default); - `StiFirstDayOfWeek::Monday` - Monday will be set as the first day of the week; - `StiFirstDayOfWeek::Sunday` - Sunday will be set as the first day of the week. |
| `formatForDateControls` | This feature allows you to customize the format for date controls. By default, the current option doesn't have a specified value, and the date format is determined based on the browser's locale. |
| `undoMaxLevel` | It sets max depth of report changes cancel when its editing. It exerts influence over memory usage. 6 changes are set by default. |
| `wizardTypeRunningAfterLoad` | It allows you to call the master of report creation after the report designer is run. It can take one of the specified below enumeration values: - `StiWizardType::None` - the report designer will be run without the invoke of report creation master (value is set by default); - `StiWizardType::StandardReport` - the report designer will be run with the invoke of standard report creation master; - `StiWizardType::MasterDetailReport` - the report designer will be run with the invoke of master-detail report creation master; - `StiWizardType::LabelReport` - the report designer will be run with the invoke of the report creation master with labels; - `StiWizardType::InvoicesReport` - the report designer will be run with the invoke of the invoice creation master; - `StiWizardType::OrdersReport` - the report designer will be run with the invoke of the order creation master; - `StiWizardType::QuotationReport` - the report designer will be run with the invoke of the quota creation master. |
| `allowWordWrapTextEditors` | It enables or disables line break in editors of text in the designer. The property has the `true` value by default. |
| `allowLoadingCustomFontsToClientSide` | Enables or disables the transfer of custom fonts to the client-side. The default value is `false`. |
| `enableShortCutKeys` | Enables or disables the handling of keyboard shortcuts. By default, this property is set to `true`. |
| `defaultRibbonType` | Allows setting the default style for the designer's toolbar. It can take one of the following values from the enumeration: - `StiDesignerRibbonType::Classic` - the classic style will be set (default value); - `StiDesignerRibbonType::SingleLine` – a compact single-line style will be set. |
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
| `showElectronicSignature` | It enables or disables the display of the **Electronic Signature** component in the toolbox or Insert tab in the designer. The property has the `true` value by default. |
| `showPdfDigitalSignature` | It enables or disables the display of the **PDF Digital Signature** component in the toolbox or Insert tab in the designer. The property has the `true` value by default. |
| `showHorizontalLinePrimitive` | It enables or disables the display of the **Horizontal Line** component in the toolbox or Insert tab in the designer. The property has the `true` value by default. |
| `showVerticalLinePrimitive` | It enables or disables the display of the **Vertical Line** component in the toolbox or Insert tab in the designer. The property has the `true` value by default. |
| `showRectanglePrimitive` | It enables or disables the display of the **Rectangle** component in the toolbox or Insert tab in the designer. The property has the `true` value by default. |
| `showRoundedRectanglePrimitive` | It enables or disables the display of the **Rounded Rectangle** component in the toolbox or Insert tab in the designer. The property has the `true` value by default. |


### dashboardElements


| **Name** | **Description** |
| --- | --- |
| `showTableElement` | It enables the display of the **Table** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showCardsElement` | It enables the display of the **Cards** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showChartElement` | It enables the display of the **Chart** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showGaugeElement` | It enables the display of the **Gauge** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showPivotTableElement` | It enables the display of the **Pivot** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showIndicatorElement` | It enables the display of the **Indicator** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showProgressElement` | It enables the display of the **Progress** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showRegionMapElement` | It enables the display of the **Region Map** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showOnlineMapElement` | It enables the display of the **Online Map** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showImageElement` | It enables the display of the **Image** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showWebContentElement` | It enables the display of the dashboard element **Web Content** in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showTextElement` | It enables the display of the **Text** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showPanelElement` | It enables the display of the **Panel** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showShapeElement` | It enables the display of the **Shape** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showButtonElement` | It enables the display of the **Button** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showListBoxElement` | It enables the display of the **List Box** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showComboBoxElement` | It enables the display of the **Combo Box** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showTreeViewElement` | It enables the display of the **Tree View** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showTreeViewBoxElement` | It enables the display of the **Tree View Box** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |
| `showDatePickerElement` | It enables the display of the **Date Picker** dashboard element in the toolbox or the **Insert** tab in the designer. The property has the `true` value by default. |


### Dictionary

| **Name** | **Description** |
| --- | --- |
| `showAdaptersInNewConnectionForm` | It enables the display of the **Object** category in the new connection creation window. The property has the `true` value by default. |
| `showDictionary` | It enables the display of the report dictionary. The property has the `true` value by default. |
| `newReportDictionary` | Allows you to use aliases in the data dictionary. It can take one of the specified below enumeration values: - `StiNewReportDictionary::Auto` - defines the mode of using aliases from a saved value in `cookies` (default value); - `StiNewReportDictionary::DictionaryNew` -  sets the mode to create a new data dictionary when creating a new report; - `StiNewReportDictionary::DictionaryMerge` - sets the mode to join the existing data dictionary with a new one when creating a new report in the designer |
| `useAliases` | It allows you to create a new data dictionary or join the existing one when creating a new report in the designer. It can take one of the specified below enumeration values: - `StiUseAliases::Auto` - defines the mode to create or join the data dictionary from a saved value in cookies (default value); - `StiUseAliases::True` - sets the mode of using aliases in the data dictionary - `StiUseAliases::False` - disables the mode of using aliases in the data dictionary. |
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
| `StiDesignerPermissions::None` | Disables any action on the item of the data dictionary. |
| `StiDesignerPermissions::Create` | It allows you to create definite element of the dictionary. |
| `StiDesignerPermissions::Delete` | It allows you to delete a definite element of the dictionary. |
| `StiDesignerPermissions::Modify` | It allows you to edit a definite element of the dictionary. |
| `StiDesignerPermissions::View` | It allows you to view a definite element of the dictionary. |
| `StiDesignerPermissions::ModifyView` | It allows you to edit and view a definite element of the dictionary. |
| `StiDesignerPermissions::All` | It allows you to make any actions on the dictionary element. |

You can configure the built-in `StiViewer` component used to preview the report. To get access to all of its settings, you should use the `viewerOptions` property, which is an object of the viewer options. All its properties are described in the [Viewer settings](../Settings.md) section. For example, you want to change the report display mode and disable unnecessary export formats:


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner;
    use Stimulsoft\Viewer\Enums\StiHtmlExportMode;
    
    $designer = new StiDesigner();
    $designer->options->viewerOptions->appearance->reportDisplayMode = StiHtmlExportMode::FromReport;
    $designer->options->viewerOptions->exports->ShowExportToWord = false;
    $designer->options->viewerOptions->exports->showExportToCsv = false;
?>
```
