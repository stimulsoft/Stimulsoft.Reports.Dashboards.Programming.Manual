# Showing Reports

> **Notice**
>
> When assigning a report viewer to a component, the report is automatically generated. Calling the `report.render()` method is necessary only if you need to perform some actions with the generated report before displaying it in the viewer.

To display a report in the viewer, simply create a `StiReport` object, load a report template into it, and assign the resulting object to the viewer. All other actions will be performed automatically; the viewer will build a report and display the first page.


**app.py**

```python

from flask import Flask, url_for, request
from stimulsoft_reports.report import StiReport
from stimulsoft_reports.viewer import StiViewer

app = Flask(__name__)

@app.route('/viewer', methods = ['GET', 'POST'])
def viewer():
    viewer = StiViewer()
    viewer.options.appearance.fullScreenMode = True

    if viewer.processRequest(request):
        return viewer.getFrameworkResponse()

    report = StiReport()
    report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
    viewer.report = report

    return viewer.getFrameworkResponse()
```

The viewer carries out the rendering of the report and is able to display both report templates and documents (generated reports). A detailed description of working with various report and document formats is found in the section [Loading and Savin a Report](../Engine/Loading_and_Saving_Report.md).
