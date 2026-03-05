# Designer Themes

The designer has the ability to change the design themes of visual controls. To do this, set the theme property in the component options.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner
from stimulsoft_reports.designer.enums import StiDesignerTheme

designer = StiDesigner()
designer.options.appearance.theme = StiDesignerTheme.OFFICE_2022_DARKGRAY_BLUE
```

Currently, there are **two themes** available, each with its own color accents. As a result, more than 50 design options are available. This allows you to customize the appearance of the designer to suit almost any web project design.
