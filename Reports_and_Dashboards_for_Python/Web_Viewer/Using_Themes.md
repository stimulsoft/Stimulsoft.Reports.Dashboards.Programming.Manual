# Appearance

The viewer has the option to change the theme of the visual control elements. To do this, simply set the `theme` property in the component options:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.viewer.enums import StiViewerTheme

viewer = StiViewer()
viewer.options.appearance.theme = StiViewerTheme.OFFICE_2022_DARKGRAY_BLUE
```

Currently, there are 8 themes available with various color accents, resulting in over 60 design options. This allows you to customize the appearance of the viewer to match almost any web project design.


### Additional Settings

By default, the viewer has only a top toolbar with all report control elements. If needed, the toolbar can be split into a top and a bottom panel. The top panel will contain the print and export menu, as well as buttons for working with parameters and bookmarks. The bottom toolbar will include page navigation controls and zoom management menus. The `displayMode` property is used to enable this mode, and it can have the following values:


| **Name** | **Description** |
| --- | --- |
| `StiToolbarDisplayMode.SIMPLE` | Simple display mode, all control elements are on one control panel (default value). |
| `StiToolbarDisplayMode.SEPARATED` | Separated display mode, the control panel is divided into a top section - for interacting with the report, and a bottom section - for interacting with the report's pages and zoom controls. |


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.options.toolbar.displayMode = StiToolbarDisplayMode.SIMPLE
viewer.options.appearance.scrollbarsMode = True
```

Additionally, there is the option to configure the appearance of the main elements of the viewer. For example, you can change the font and color of the toolbar labels, set the background of the viewer, specify the page border color, and more. Below is a list of available properties for customizing the viewer’s appearance and their default values:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()

viewer.options.appearance.backgroundColor = 'white'
viewer.options.appearance.pageBorderColor = 'gray'
viewer.options.appearance.showPageShadow = False

viewer.options.toolbar.backgroundColor = 'transparent';
viewer.options.toolbar.borderColor = 'transparent';
viewer.options.toolbar.fontColor = 'transparent';
viewer.options.toolbar.fontFamily = 'Arial';
```


For color values, you can specify either one of the standard HTML color constants or a color code in RGB format, such as '`#ff2020`'.
