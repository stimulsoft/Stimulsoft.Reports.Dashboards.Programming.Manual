# Viewing Modes

The viewer allows configuring various interface and report page display modes, as well as controlling the display on mobile devices.


### Scrollbars

The viewer offers two report display modes: with and without scrollbars. By default, the mode without scrollbars is enabled. To enable the scrolling mode, simply set the `scrollbarsMode` property to `true`.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->appearance->scrollbarsMode = true;
?>
```

In the first mode (without scrollbars), the viewer displays the page or report in full, automatically resizing the viewing area. If width and height are set, the viewer will crop any parts of the page that exceed these boundaries. In the second mode, scrollbars will appear when the page exceeds the viewer's dimensions, allowing users to scroll and view the entire report without cropping.


> **Information**
>
> When using the scrollbars mode, you need to specify the viewer's height. If no height is set, the default height will be 650 pixels.

**Full-Screen mode**

The viewer supports full-screen mode for viewing reports and dashboards. By default, the standard viewing mode is enabled with predefined dimensions. To enable full-screen mode, set the `fullScreenMode` property to `true`.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->appearance->fullScreenMode = true;
?>
```

Alternatively, full-screen mode can be toggled using the button on the viewer's control panel.

**Report page display modes**

The viewer supports three modes for displaying reports: page-by-page display, continuous scroll (report as a strip) and table of pages display. To control these modes, use the `viewMode` property, which accepts one of the corresponding values.


| **Name** | **Description** |
| --- | --- |
| `StiWebViewMode::SinglePage` | Displays a single page selected from the toolbar. |
| `StiWebViewMode::Continuous` | Displays all report pages as a continuous strip. |
| `StiWebViewMode::MultiplePages` | Displays all report pages in a table format. |

For example, to enable the continuous scroll mode:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Viewer\Enums\StiWebViewMode;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->viewMode = StiWebViewMode::Continuous;
?>
```

**Mobile mode**

The viewer is designed to support both desktop and mobile devices, including touchscreen functionality. To control the interface modes, use the `interfaceType` property, which accepts one of the following values:


| **Name** | **Description** |
| --- | --- |
| `StiInterfaceType::Auto` | The viewer interface type will be automatically selected based on the device in use (default value). |
| `StiInterfaceType::Mouse` | Forced use of the standard interface for viewer control via mouse. |
| `StiInterfaceType::Touch` | Forced use of the `Touch` interface for control via a touchscreen monitor, where viewer interface elements are enlarged for easier control. |
| `StiInterfaceType::Mobile` | Forced use of the `Mobile` interface for control via a smartphone screen, where the viewer interface is simplified and adapted for mobile device control. |

For example, to completely disable mobile mode:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Viewer\Enums\StiInterfaceType;
    
    $viewer = new StiViewer();
    $viewer->options->appearance->interfaceType = StiInterfaceType::Mouse;
?>
```
