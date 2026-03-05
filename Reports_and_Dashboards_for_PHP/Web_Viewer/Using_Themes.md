# Appearance

The viewer offers the ability to change the visual themes of the control elements. To do this, simply set the `theme` property in the component's options:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Viewer\Enums\StiViewerTheme;
    
    $viewer = new StiViewer();
    $viewer->options->appearance->theme = StiViewerTheme::Office2022BlackGreen;
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).


Currently, there are **8** available themes with different color accents, resulting in over **60** layout options. This flexibility allows you to customize the viewer's appearance to match virtually any web project design.


**Additional settings**

By default, the viewer has only a top toolbar, which contains all the report control elements. If needed, the toolbar can be split into an upper and a lower toolbar. The upper toolbar will contain the print and export menu, along with buttons for working with parameters and bookmarks. The lower toolbar will include page navigation elements and zoom control. To enable this mode, use the **displayMode** property, which can have the following values:


| **Name** | **Description** |
| --- | --- |
| `StiToolbarDisplayMode::Simple` | Simple display mode, all control elements are located on a single toolbar (this is the default setting). |
| `StiToolbarDisplayMode::Separated` | Split display mode. The toolbar is divided into an upper section for interacting with the report and a lower section for interacting with the pages. |


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Viewer\Enums\StiToolbarDisplayMode;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->displayMode = StiToolbarDisplayMode::Simple;
    $viewer->options->appearance->scrollbarsMode = true;
?>
```

Additionally, you can customize the design of the viewer's core elements. For example, you can change the font and color of the viewer's toolbar text, set the background color, specify the page border color, and more. Below is a list of available properties for customizing the viewer's appearance and their default values:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    
    $viewer->options->appearance->backgroundColor = 'white';
    $viewer->options->appearance->pageBorderColor = 'red';
    $viewer->options->appearance->showPageShadow = false;
    
    $viewer->options->toolbar->backgroundColor = 'aqua';
    $viewer->options->toolbar->borderColor = 'darkgreen';
    $viewer->options->toolbar->fontColor = 'white';
    $viewer->options->toolbar->fontFamily = 'Arial';
?>
```

For color values, you can use either standard HTML color constants or a color code in RGB format, such as `#ff2020`.
