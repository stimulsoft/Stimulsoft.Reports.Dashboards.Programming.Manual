# Localization

The viewer fully supports localization of its interface. To localize the interface to the desired language, simply set the required filename for the `localization` option in the viewer:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->localization = 'de.xml';
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).


All available localization XML files are located in the resources of the installed product package. If necessary, a localization file can be loaded from any other location by specifying the full path to the desired XML file in the `localization` option.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->localization = '/resources/loc/de.xml';
?>
```
