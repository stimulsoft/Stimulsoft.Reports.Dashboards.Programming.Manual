# Settings

The **HTML5 Designer** configuration is done using properties that are located in the **StiNetCoreDesignerOptions** class. All properties are divided into groups, some of the groups contain subgroups of properties for ease of use. Below is an example of setting some properties of the designer.


**Index.cshtml**

```
...
@Html.StiNetCoreDesigner(new StiNetCoreDesignerOptions() {
    Theme = Stimulsoft.Report.Web.StiDesignerTheme.Office2022WhiteTeal,
    Localization = "Localization/en.xml",
    Actions =
    {
        GetReport = "GetReport",
        PreviewReport = "PreviewReport",
        SaveReport = "SaveReport",
        DesignerEvent = "DesignerEvent"
    },
    Appearance =
    {
        InterfaceType = StiInterfaceType.Auto,
        ShowTooltipsHelp = false,
        ShowDialogsHelp = false,
        DefaultUnit = Stimulsoft.Report.StiReportUnitType.Centimeters
    },
    Dictionary =
    {
        PermissionBusinessObjects = Stimulsoft.Report.Web.StiDesignerPermissions.None,
        PermissionDataConnections = Stimulsoft.Report.Web.StiDesignerPermissions.View
    },
    Bands =
    {
        ShowChildBand = false,
        ShowEmptyBand = false,
        ShowOverlayBand = false
    }
})
...
```

### Basic settings (without groups)

| **Name** | **Description** |
| --- | --- |
| Theme | Specifies the [theme of the report designer](Using_Themes.md). The list of available themes is located in the **StiDesignerTheme** enumeration. The default value is **Office2022WhiteBlue**. |
| Localization | Specifies the path to the [XML localization file](Localization.md). The path can be absolute or relative. By default, English localization is used. It is built into the designer and does not require additional XML files. |
| LocalizationDirectory | Specifies the path to the directory with [XML localization files](Localization.md). The localization files located in the specified folder will be loaded to the localization list in the designer panel. |
| Width | Sets the width of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. By default, the component is expanded to the entire area of the browser window. |
| Height | Sets the height of the component in the required units that are specified in the **Unit** class. The value can be set in pixels - **Unit.Pixel()**, points - **Unit.Point()** and per cent - **Unit.Percentage()**. By default, the component is expanded to the entire area of the browser window. |


### Actions

| **Name** | **Description** |
| --- | --- |
| GetReport | Specifies the name of the action method to prepare [the report template when loading the designer](Add_Designer.md). |
| OpenReport | Specifies the name of the action method to open the report template from the designer menu. |
| CreateReport | Specifies the name of the action method to prepare the report template when [creating the new report in the designer](Creating_Report.md). |
| SaveReport | Specifies the name of the action method [to save the report template](Save_Report.md) on the server side.. |
| SaveReportAs | Specifies the name of the action method to store the report template on the server side when using the **Save As** menu item. If no action is specified, the built-in method of saving [the report template](Save_Report.md) to the local disk will be used. |
| PreviewReport | Specifies the name of the action method to prepare the rendered report [in the preview window](Preview.md). |
| GetPreviewReport | Specifies the name of the action method just before a report is displayed in [the preview window](Preview.md). |
| ExportReport | Specifies the name of the action method [to export reports](Additional_Functionality_of_Preview.md) to the specified format. |
| Exit | Specifies the name of the action method to go to the desired view by clicking [the Exit button](Events.md) in the main menu of the report designer. |
| DesignerEvent | Specifies the name of the action method of the report designer to handle [additional designer actions](Events.md), such as working with data, report components, and others. Also, this action is used to load scripts and designer styles. |


### Server

| **Name** | **Description** |
| --- | --- |
| RouteTemplate | Sets the route template that is returned when the report designer actions are executed. If the property is not set, then the Razor project template will be used instead. If the `UseRelativeUrls` property is set to `true`, the `BasePath` will not be respected for this property.The default value of this property is null. |
| ShowServerErrorPage | Enables the display of an HTML page with error details that occurred on the server side. The error details will be displayed in the preview window if the property is enabled. If the property is disabled, the numeric error code and a short error description will be displayed in the dialog window. By default, the property is set to **true**. |
| AllowAutoUpdateCookies | Allows the designer to update the cookies automatically on every request to the server. By default, cookies are set when creating the designer, if they are not specified in the report. By default, the property is set to **false**. |
| AllowAntiforgeryToken | Allow the designer to automatically request and send the antiforgery token. By default, the property is set to **true**. |
| RequestTimeout | Sets the time to wait for a response from the server in seconds, after which an error will be generated. The default value is 30 seconds. For big reports, it is recommended to increase this value. |
| CacheTimeout | Sets the time in minutes that the server will store the rendered report since the last action of the viewer. The default setting is 10 minutes. |
| CacheMode | Sets the report caching mode. It can take one of the following values of the **StiServerCacheMode** enumeration: **None** – caching is disabled in **HTML5 Designer**; **ObjectCache** – the cache is used as the storage, the report is stored as an object (default value); **ObjectSession** – the session is used as the storage, the report is stored as an object; **StringCache** – the server cache is used as the storage, the report is serialized to a packed string; **StringSession** – the session is used as a repository, the report is serialized into a packed string. |
| CacheItemPriority | Sets the priority of the report stored in the server cache. This property affects the automatic clearing of the server memory in case of lack of memory. The lower the priority is, the greater is the chance of removing information from memory. |
| AllowAutoUpdateCache | Sets the mode for automatic cache update. The report stored in the cache or server session will be automatically re-saved after a certain period of time if the designer is idle (about every 3 minutes). By default, the property is set to **true**. |
| UseRelativeUrls | Sets the designer mode in which relative URLs are used for requests to the server. By default, the property is set to **true**. |
| PortNumber | Gets or sets a value which specifies the port number to use in the URL. A value of **0** defines automatic detection (default value). A value of **-1** removes the port number. |
| PassQueryParametersForResources | Enables transferring all request URL parameters when generating links to the resources of the designer. If **false**, only the necessary parameters are used to request the resources of the designer. This corresponds to the more correct operation of the browser cache. By default, the property is set to **true**. |
| PassFormValues | Enables transferring the POST form values to the client side, if these values are to be used in the actions of the designer. If you enable this feature, the additional **GetFormValues()** method will return a collection of form parameters. By default, the property is **false**. |
| UseCompression | Enables compression of designer requests in the GZip stream. This allows you to reduce the amount of Internet traffic, but slows down the designer. By default, the property is **false**. |
| UseCacheForResources | Enables caching of the component resources on the server side. The following resources are supported: scripts, styles and images. This option improves the load speed of the component and also reduces the server load in multi-client environments. The default value is **true**. |
| AllowLoadingCustomFontsToClientSide | Allows you to pass custom fonts to the client side and convert them to CSS style for the correct display of text as HTML with a specified font. By default, the property is set to **false**. |


### Appearance

| **Name** | **Description** |
| --- | --- |
| CustomCss | Specifies the path to the CSS file of styles for the report designer. If this property is set, the standard styles of the selected theme will not be loaded. The default value is an empty value. |
| DefaultUnit | Sets the units for the size of the report and all its components. By default, centimeters are used. |
| Zoom | Sets the zoom for displaying report pages. The default setting is 100 percent. It can take one of the following values of the **StiZoomMode** enumeration: **PageWidth** – when the designer runs, the zoom, necessary to display the report by the page width, will be set; **PageHeight** – when the designer runs, the zoom, required to display the page height of the report, will be set. |
| ShowAnimation | Enables animation for various elements of the designer interface. By default, the property is set to **true**. |
| ShowOpenDialog | Allows to display the open dialog, or to open with the open event. By default, the property is set to **true**. |
| ShowTooltips | Enables displaying tooltips for designer controls when the mouse hovers over. By default, the property is set to **true**. |
| ShowTooltipsHelp | Enable displaying links to online documentation in tooltips for designer controls. By default, the property is set to **true**. |
| ShowDialogsHelp | Enables displaying links to online documentation on the titles of dialog forms of the designer. By default, the property is set to **true**. |
| InterfaceType | Sets the type of interface used for the designer. It can take one of the following **StiInterfaceType** enumeration values: **Auto** – the interface type of the designer will be selected automatically depending on the device used (default value); **Mouse** – forced use of the interface to control the designer with the mouse; **Touch** – forced use of the Touch interface to control the designer via the touch screen (mobile devices), also in this mode, the interface elements are increased. |
| DatePickerFirstDayOfWeek | Sets the first day of the week for the select date item. It can take one of the following values of the **StiFirstDayOfWeek** enumeration: **Auto** – automatic detection of the first day of the week from the browser settings (default value); **Monday** – the first day of the week is Monday; **Sunday** – the first day of the week is Sunday. |
| DatePickerIncludeCurrentDayForRanges | Sets a value, which indicates that the current day will be included in the ranges of the date picker. By default, the property is set to **false**. |
| FormatForDateControls | This feature allows you to customize the format for date controls. By default, the current option does not have a specified value, and the date format is determined based on the browser's locale. |
| ShowReportTree | Enables displaying the tree of report components. By default, the property is set to **true**. |
| ChartRenderType | Gets or sets the type of the chart in the preview. It can take one of the following **StiChartRenderType** enumeration values: **Image** – charts are displayed as static images; **Vector** – charts are displayed in the vector mode as an SVG object; **AnimatedVector** - charts are displayed in the vector mode as an SVG object, the chart elements are displayed with animation (default value). |
| ReportDisplayMode | Sets the export mode for displaying report pages in the preview tab. Can take one of the following values of the **StiReportDisplayMode** enumeration: **FromReport** - the export mode of the report elements is defined from report template settings - Div or Table; **Table** – report elements are exported using HTML tables (default value); **Div** – report elements are exported using DIV markup; **Span** - report items are exported using SPAN markup. |
| ParametersPanelDateFormat | Sets the date and time format for variables of the corresponding type in the parameters panel. By default, the date and time format set by the browser is used. |
| CloseDesignerWithoutAsking | Sets a value which indicates that the designer will be closed without asking. By default, the property is set to **true**. |
| ShowSystemFonts | Sets a visibility of the system fonts in the fonts list. By default, the property is set to **true**. |
| WizardTypeRunningAfterLoad | Calls the Report wizard after starting the report designer. It may have one of the following **StiWizardType** enumeration values: **None** - runs the report designer without running the report wizard; **StandardReport** - runs the Standard wizard; **MasterDetailReport** - runs the Master-Detail wizard; **LabelReport** - runs the Label wizard; **InvoicesReport** - runs the Invoice wizard; **OrdersReport** - runs the Order wizard; **QuotationReport** - runs the Quote wizard. |
| AllowWordWrapTextEditors | Allows word wrap in the text editors. By default, the property is set to **true**. |
| DefaultRibbonType | Allows setting the default style for the designer's toolbar. It can take one of the following values from the enumeration: **StiDesignerRibbonType.Classic** - the classic style will be set (default value); **StiDesignerRibbonType.SingleLine** – a compact single-line style will be set. |
| AllowPropagationEvents | Allows the propagation of key press events when the report designer is not in focus. By default, the property is set to **true**. |
| PropertiesPanelViewMode | Provides the ability to pin or unpin the Properties panel, Report Dictionary, and Report Tree. It can take one of the following values from the enumeration: **Pinned** — panels are pinned (default value); **Unpinned** — panels are unpinned. |


### Behavior

| **Name** | **Description** |
| --- | --- |
| ShowSaveDialog | Enables displaying the dialog to insert a report name when it is saved. The name of the report will be transferred in the parameters of the report designer. By default, the property is set to **true**. |
| UndoMaxLevel | Sets the maximum number to cancel actions with the report (the Undo/Redo function). A big value of this property will consume memory on the server side to store the undo parameters. The default value is **6**. |
| AllowChangeWindowTitle | Allows using the title of the browser window to display the file name of the edited report. By default, the property is set to **true**. |
| SaveReportMode | Sets the mode to save the report. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (default value); **Visible** - saving of the report is called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report is called in a new window (tab) of the web browser. |
| SaveReportAsMode | Sets the mode for saving the report. It has the three values of the **StiSaveMode** enumeration. **Hidden** - saving of the report is called in the background mode using the AJAX request and is not shown in the browser window (default value); **Visible** - saving of the report is called in the current web browser window in the visible mode using the POST request; **NewWindow** - saving of the report is called in a new window (tab) of the web browser. |
| CheckReportBeforePreview | Sets the value that allows running the report checker before preview. |


### FileMenu

| Name | Description |
| --- | --- |
| Visible | Enables displaying the main menu of the report designer. By default, the property is set to **true**. |
| ShowNew | Enables showing the main menu item - **New**. By default, the property is set to **true**. |
| ShowFileMenuNewReport | Sets a visibility of the new report button in the designer. By default, the property is set to **true**. |
| ShowFileMenuNewDashboard | Sets a visibility of the new dashboard button in the designer. By default, the property is set to **true**. |
| ShowOpen | Enables showing the main menu item - **Open**. By default, the property is set to **true**. |
| ShowSave | Enables showing the main menu item - **Save**. By default, the property is set to **true**. |
| ShowSaveAs | Enables showing the main menu item - **Save As**. By default, the property is set to **true**. |
| ShowClose | Enables showing the main menu item - **Close**. By default, the property is set to **true**. |
| ShowExit | Enables showing the main menu item - **Exit**. By default, the property is set to **false**. |
| ShowReportSetup | Enables showing the main menu item - **Report Setup**. By default, the property is set to **true**. |
| ShowOptions | Enables showing the main menu item - **Options**. By default, the property is set to **true**. |
| ShowInfo | Enables showing the main menu item - **Info**. By default, the property is set to **true**. |
| ShowAbout | Enables showing the main menu item - **About**. By default, the property is set to **true**. |
| ShowHelp | Enables showing the main menu item - **Help**. By default, the property is set to **true**. |


### Dictionary

| **Name** | **Description** |
| --- | --- |
| Visible | Enables showing the data dictionary of the report. By default, the property is set to **true**. |
| UseAliases | Allows you to use aliases in the data dictionary. It has the three values of the **StiUseAliases** enumeration: **Auto** - defines the mode of using aliases from a saved value in cookies (default value); **True** - sets the mode of using aliases in the data dictionary; **False** - disables the mode of using aliases in the data dictionary. |
| NewReportDictionary | It allows you to create a new data dictionary or join the existing one when creating a new report in the designer. It has the three values of the **StiNewReportDictionary** enumeration: **Auto** - defines the mode to create or join the data dictionary from a saved value in cookies (default value); **DictionaryNew** - sets the mode to create a new data dictionary when creating a new report; **DictionaryMerge** - sets the mode to join the existing data dictionary with a new one when creating a new report in the designer. |
| ShowDictionaryContextMenuProperties | Sets a visibility of the **Properties** item in the dictionary context menu. By default, the property is set to **true**. |
| ShowDictionaryActions | Sets a visibility of the **Actions** **menu** on the dictionary toolbar. By default, the property is set to **true**. |
| PermissionDataConnections | Sets the available actions to connect data to the report. It can take one or more values from the **StiDesignerPermissions** enumeration. |
| PermissionDataSources | Sets available actions on report data sources. It can take one or more values from the **StiDesignerPermissions** enumeration. |
| PermissionDataColumns | Sets the available actions on data columns in the report. It can take one or more values from the **StiDesignerPermissions** enumeration. |
| PermissionBusinessObjects | Sets the available actions on the business objects in the report. It can take one or more values from the **StiDesignerPermissions** enumeration. |
| PermissionDataRelations | Sets the available actions to linking data in the report. It can take one or more values from the **StiDesignerPermissions** enumeration. |
| PermissionVariables | Sets available actions on report variables. It can take one or more values from the **StiDesignerPermissions** enumeration. |
| PermissionResources | Sets the available actions for the resources in the Report Dictionary. Takes one or several values from the **StiDesignerPermissions** enumeration. |
| PermissionSqlParameters | Sets the available actions for the parameters of the SQL queries for the Report DataSources. Takes one or several values from **StiDesignerPermissions** enumeration. |
| PermissionDataTransformations | Sets the available actions on data transformation. It can take one or more values from the **StiDesignerPermissions** enumeration. |
| PermissionUserFunctions | Sets the available actions for the user functions. It can take one or more values from the **StiDesignerPermissions** enumeration. |

The table below shows all available values for the **StiDesignerPermissions** enumeration, which can be set for the dictionary elements of the report.


| **Value** | **Description** |
| --- | --- |
| None | Disables any action on the item of the data dictionary. |
| All | Allows any action on the item of the data dictionary. |
| Create | Allows creating a specific data dictionary item. |
| Delete | Allows deleting a specific data dictionary item. |
| Modify | Allows modifying a specific data dictionary item. |
| View | Allows viewing a specific data dictionary item. |
| ModifyView | Allows modifying and viewing a specific data dictionary item. |


### Toolbar

| **Name** | **Description** |
| --- | --- |
| ShowToolbar | Enables displaying the toolbar of the designer. By default, the property is set to **true**. |
| ShowSetupToolboxButton | Enables displaying the button to call the dialog box with settings for the side toolbar. By default, the property is set to **true**. |
| ShowInsertButton | Enables displaying the  **Insert** tab on the toolbar of the designer. By default, the property is set to **true**. |
| ShowLayoutButton | Enables displaying the tab **Layout** tab on the toolbar of the designer. By default, the property is set to **true**. |
| ShowPageButton | Enables displaying the tab **Page** tab on the toolbar of the designer. By default, the property is set to **true**. |
| ShowPreviewButton | Enables displaying the tab **Preview** tab on the toolbar of the designer. By default, the property is set to **true**. |
| ShowSaveButton | Enables displaying the **Save** button on the toolbar of the designer. By default, the property is set to **true**. |
| ShowAboutButton | Enables displaying the **About** on the toolbar of the designer. By default, the property is set to **false**. |


### PropertiesGrid

| **Name** | **Description** |
| --- | --- |
| Visible | Enables displaying the property panel. By default, the property is set to **true**. |
| Width | Sets the width of the property panel. By default, the width is set to **370 px**. |
| LabelWidth | Specifies the width of the labels on the properties panel. By default, the width is set to **160 px**. |
| PropertiesGridPosition | Sets **Left** or **Right** position of the properties grid in the designer. It has the three values of the **StiPropertiesGridPosition** enumeration: **Left**; **Right**. |
| ShowPropertiesWhichUsedFromStyles | Sets a visibility of the properties which used from styles in the designer. By default, the property is set to **false**. |


### Components

| **Name** | **Description** |
| --- | --- |
| ShowText | Enables displaying the **Text** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowTextInCells | Enables displaying the **Text in Cells** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowRichText | Enables displaying the **Rich Text** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowImage | Enables displaying the **Image** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowBarCode | Enables displaying the **Bar Code** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowShape | Enables displaying the **Shape** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowHorizontalLinePrimitive | Enables displaying the **Horizontal Line** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowVerticalLinePrimitive | Enables displaying the **Vertical Line** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowRectanglePrimitive | Enables displaying the **Rectangle** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowRoundedRectanglePrimitive | Enables displaying the **Rounded Rectangle** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowPanel | Enables displaying the **Panel** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowClone | Enables displaying the **Clone** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowCheckBox | Enables displaying the **Check Box** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowSubReport | Enables displaying the **Sub Report** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowZipCode | Enables displaying the **Zip Code** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowTable | Enables displaying the **Table** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowCrossTab | Enables displaying the **Cross-Tab** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowChart | Enables displaying the **Chart** component in the insert menu for report components. It affects on all chart types. By default, the property is set to **true**. |
| ShowMap | Enables displaying the **Map** component in the insert menu for report components. By default, the property is set to **false**. |
| ShowGauge | Enables displaying the **Gauge** component in the insert menu for report components. By default, the property is set to **false**. |
| ShowSparkline | Enables displaying the **Sparkline** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowMathFormula | Enables displaying the **Math Formula** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowElectronicSignature | Enables displaying the **Electronic Signature** component in the insert menu for report components. By default, the property is set to **true**. |
| ShowPdfDigitalSignature | Enables displaying the **PDF Digital Signature** component in the insert menu for report components. By default, the property is set to **true**. |


### Bands

| **Name** | **Description** |
| --- | --- |
| ShowReportTitleBands | Enables displaying the **Report Title** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowReportSummaryBand | Enables displaying the **Report Summary** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowPageHeaderBand | Enables displaying the **Page Header** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowPageFooterBand | Enables displaying the **Page Footer** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowGroupHeaderBand | Enables displaying the **Group Header** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowGroupFooterBand | Enables displaying the **Group Footer** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowHeaderBand | Enables displaying the **Header** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowFooterBand | Enables displaying the **Footer** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowColumnHeaderBand | Enables displaying the **Column Header** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowColumnFooterBand | Enables displaying the **Column Footer** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowDataBand | Enables displaying the **Data** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowHierarchicalBand | Enables displaying the **Hierarchical** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowChildBand | Enables displaying the **Child** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowEmptyBand | Enables displaying the **Empty** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowOverlayBand | Enables displaying the **Overlay** item in the **Bands** menu of the designer. By default, the property is set to **true**. |
| ShowTableOfContents | Enables displaying the **Table of Contents** item in the **Bands** menu of the designer. By default, the property is set to **true**. |


### DashboardElements

| Name | Description |
| --- | --- |
| ShowTableElement | Enables displaying the **Table** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowCardsElement | Enables displaying the **Cards** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowChartElement | Enables displaying the **Chart** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowGaugeElement | Enables displaying the **Gauge** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowPivotTableElement | Enables displaying the **Pivot** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowIndicatorElement | Enables displaying the **Indicator** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowProgressElement | Enables displaying the **Progress** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowRegionMapElement | Enables displaying the **Region Map** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowOnlineMapElement | Enables displaying the **Online Map** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowImageElement | Enables displaying the **Image** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowTextElement | Enables displaying the **Text** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowPanelElement | Enables displaying the **Panel** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowShapeElement | Enables displaying the **Shape** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowButtonElement | Enables displaying the **Button** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowListBoxElement | Enables displaying the **List Box** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowComboBoxElement | Enables displaying the **Combo Box** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowTreeViewElement | Enables displaying the **Tree View** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowTreeViewBoxElement | Enables displaying the **Tree View Box** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |
| ShowDatePickerElement | Enables displaying the **Date Picker** element in the Dashboard Elements menu of the designer. By default, the property is set to **true**. |


### CrossBands

| **Name** | **Description** |
| --- | --- |
| ShowCrossGroupHeaderBand | Enables displaying the **Cross Group Header** section in the insert menu for report components. By default, the property is set to **true**. |
| ShowCrossGroupFooterBand | Enables displaying the **Cross Group Footer** section in the insert menu for report components. By default, the property is set to **true**. |
| ShowCrossHeaderBand | Enables displaying the **Cross Header** section in the insert menu for report components. By default, the property is set to **true**. |
| ShowCrossFooterBand | Enables displaying the **Cross Footer** section in the insert menu for report components. By default, the property is set to **true**. |
| ShowCrossDataBand | Enables displaying the **Cross Data** section in the insert menu for report components. By default, the property is set to **true**. |

**Dashboards**


**Name
              
              
                Description

                ShowNewDashboardButton
              
              
                Sets a visibility of the New Dashboard button in the designer. By default, the property is set to true.**

**Pages**


**Name
              
              
                Description

                ShowNewPageButton
              
              
                Sets a visibility of the New Page button in the designer. By default, the property is set to true.**

When designing a report or dashboard in the report designer, you can also define **ExportOptions**, **EmailOptions**, and **PreviewToolbarOptions** on the **Preview** tab. These options are similar to the [report viewer options](../Using_Web_Viewer/Settings.md).
