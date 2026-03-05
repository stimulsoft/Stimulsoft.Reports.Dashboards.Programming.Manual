# Localization

The designer fully supports localization of its interface. To localize the interface in the desired language, you only need to set the required file name for the `localization` option in the designer:


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner; 
    
    $designer = new StiDesigner();
    $designer->options->localization = 'de.xml';
    $designer->printHtml();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Designer/Localizing%20the%20Designer.php).


All available localization XML files can be found in the resources of the installed product package. If necessary, the localization file can be loaded from any other location by specifying the full path to the required XML file for the `localization` option:


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner; 
    
    $designer = new StiDesigner();
    $designer->options->localization = '/resources/loc/de.xml';
    $designer->printHtml();
?>
```

The designer also provides the ability to choose the necessary interface localization via a special menu in the toolbar. By default, this menu includes the English (built-in) localization as well as the one set via the `localization` property. To add additional localizations to the menu, a special method `addLocalization()` is available in the designer options. You can specify the localization file or the full path to this file as a parameter.


Example of adding additional localizations located in the component resources:


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner; 
    
    $designer = new StiDesigner();
    $designer->options->localization = 'de.xml';
    $designer->options->addLocalization('fr.xml');
    $designer->options->addLocalization('es.xml');
    $designer->options->addLocalization('pt.xml');
    $designer->printHtml();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Designer/Localizing%20the%20Designer.php).
