# Creating and Editing Reports

No action is needed to start the designer without a report. Once the component is loaded, the main designer menu will appear. If you wish to initiate the designer with a new (empty) report, you can create a new `StiReport` report object and allocate it to the designer.


For editing a report within the designer, just create a `StiReport` object, load a report template into it, and assign the resulting object to the designer. All other actions will occur automatically; the designer will showcase the first page of the template.


**app.py**

```python

from flask import Flask, url_for, request
from stimulsoft_reports.report import StiReport
from stimulsoft_reports.designer import StiDesigner

app = Flask(__name__)

@app.route('/designer', methods = ['GET', 'POST'])
def designer():
    designer = StiDesinger()
    designer.options.appearance.fullScreenMode = True

    if designer.processRequest(request):
        return designer.getFrameworkResponse()

    report = StiReport()
    report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
    designer.report = report

    return designer.getFrameworkResponse()
```

The designer is equipped to handle standard, packaged, and encrypted templates. Detailed instructions on working with various report formats are provided in the [Loading and Saving Reports](../Engine/Loading_and_Saving_Report.md) section.

### Report creation event

A new report can be generated using the main menu of the designer. To preload data for a new report or execute any other necessary actions with a new report, the `onCreateReport` event is utilized. This event will be activated when a new empty report is created from the main menu or when a report is generated using the wizard.


Within an event on the Python server side, modifications to the report or its parameters are permitted.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner
from stimulsoft_reports.events import StiReportEventArgs

def createReport(args: StiReportEventArgs):
    args.report['ReportDescription'] = 'This is a report description from the Python server-side.'

designer = StiDesigner()
designer.onCreateReport += createReport
```

All functionalities of the reporting tool are accessible in the client-side JavaScript event. For instance, you can link data for a new report and synchronize it with a dictionary.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner

designer = StiDesigner()
designer.onCreateReport += 'createReport'
```


**designer.html**

```html

<script>
    function createReport(args) {
        let dataSet = new Stimulsoft.System.Data.DataSet("Demo");
        dataSet.readJsonFile("/static/data/Demo.json");
        
        let report = args.report;
        report.regData(dataSet.dataSetName, "", dataSet);
        report.dictionary.synchronize();
    }
</script>
```

A detailed description of the available argument values is in the [Designer Events](Events.md) section.
