# Localization

The designer supports full localization of its interface. To localize the interface into the required language, just set the required file name for the `localization` option in the designer:


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner

designer = StiDesigner()
designer.options.localization = 'de.xml'
```

All available localization XML files are located in the resources of the installed product package. If necessary, the localization file can be loaded from any other location; for this you need to specify the full path to the desired XML file for the `localization` option:


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner

designer = StiDesigner()
designer.options.localization = '/resources/loc/de.xml'
```

If the file is readable from the Python application, the localization will load into the designer. Otherwise, the built-in English localization of the interface will be used.


The designer provides the option to select the necessary interface localization using a special menu on the toolbar. By default, English (built-in) localization is included in this menu, as well as any specified using the `localization` property. To add additional localizations to the menu, there's a special designer option, `localization`, which is a collection of localizations. The localization file or the full path to this file is specified as values.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner

designer = StiDesigner()
designer.options.localization = 'de.xml'
designer.options.localizations.append('fr.xml')
designer.options.localizations.append('pl.xml')
designer.options.localizations.append('/resources/loc/it.xml')
```
