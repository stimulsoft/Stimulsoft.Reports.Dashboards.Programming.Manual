# Localization

The viewer supports full localization of the UI. To localize the interface into the required language, just set the required file name for the `localization` option in the viewer:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.options.localization = 'de.xml'
```

The localization XML files can be found in the resources of the installed product package. If necessary, the localization file can be loaded from any other location; for this you need to specify the full path to the desired XML file for the `localization` option:


**app.py**

from stimulsoft_reports.viewer import StiViewer
viewer = StiViewer()viewer.options.localization = '/resources/loc/de.xml'

If the file is readable from the Python application, the localization will be loaded into the viewer. Otherwise, the built-in English localization of the interface will be used.
