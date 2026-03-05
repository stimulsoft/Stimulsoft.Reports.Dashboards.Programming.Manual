# Display Modes

The viewer allows configuring various interface and report page display modes, as well as managing the display on mobile devices.


### Scrollbars

The viewer offers two report display modes: with scrollbars and without them. By default, the mode without scrollbars is enabled. To enable the mode with scrollbars, simply set the `scrollbarsMode` property to `True`.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.appearance.scrollbarsMode = True
```

In the first mode (without scrollbars), the viewer displays the page or report in its entirety, automatically stretching the viewing area. If width and height dimensions are specified, the viewer will crop any content that extends beyond the page boundaries. In the second mode, unlike the first, no cropping occurs when the page extends beyond the viewer's dimensions. Instead, scrollbars appear, allowing the user to scroll through the page or report.


> **Information**
>
> Using the report viewing mode with scrollbars, the height of the viewer must be set, otherwise, a default height of 650 pixels will be applied.

### Fullscreen mode

The viewer includes a fullscreen mode for displaying reports and dashboards. By default, the standard viewing mode is enabled, with the viewer sized according to the settings. To enable fullscreen mode, simply set the `fullScreenMode` property to `True`.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.appearance.fullScreenMode = True
```

To enable or disable fullscreen mode, you can also use the corresponding button on the viewer's control panel.

### Report page display

The viewer offers three report display modes:

- Single-page display;
- Continuous display of the entire report as a scrollable ribbon;
- Table display of report pages.


The property `viewMode` is used to control these modes, and it accepts one of the following values:


| **Name** | **Description** |
| --- | --- |
| `StiWebViewMode.SINGLE_PAGE` | Displays one page selected from the toolbar. |
| `StiWebViewMode.CONTINUOUS` | Displays all report pages as a continuous ribbon. |
| `StiWebViewMode.MULTIPLE_PAGES` | Displays all report pages in a table format. |

For example, to set the mode to display all pages as a continuous ribbon:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.viewer.enums import StiWebViewMode

viewer = StiViewer()
viewer.toolbar.viewMode = StiWebViewMode.CONTINUOUS
```

### Mobile mode

The viewer supports both desktop and touchscreen mobile devices. To control the interface modes, use the `interfaceType` property, which accepts one of the following values:


| **Name** | **Description** |
| --- | --- |
| `StiInterfaceType.AUTO` | The viewer's interface type will be automatically selected based on the device being used (default value). |
| `StiInterfaceType.MOUSE` | Forces the use of the standard interface for controlling the viewer with a mouse. |
| `StiInterfaceType.TOUCH` | Forces the use of the Touch interface for controlling the viewer with a touchscreen. In this mode, the viewer's interface elements are larger for easier interaction. |
| `StiInterfaceType.MOBILE` | Forces the use of the Mobile interface for controlling the viewer via a smartphone screen. In this mode, the viewer interface is simplified and adapted for mobile device control. |

For example, to completely disable the mobile display mode:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.viewer.enums import StiInterfaceType

viewer = StiViewer()
viewer.appearance.interfaceType = StiInterfaceType.MOUSE
```
