# Report Rendering

To build a loaded report, you need to call the `render()` function on the `StiReport` report object. For example, you need to build a report before exporting it:


**app.py**

```python

from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiExportFormat

report = StiReport()
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
report.exportDocument(StiExportFormat.PDF)
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


If it is necessary to perform any actions with the report before it is rendered using JavaScript code, simply define the name of the JavaScript function for the `onBeforeRender` event. The function will receive the action type and the report itself as arguments. Example of registering JSON data before the report is rendered:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.onBeforeRender += 'beforeRender'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**render.html**

```html

<script>
    function onBeforeRender(args) {
        var dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
        dataSet.readJsonFile("Demo.json");
        
        var report = args.report;
        report.regData(dataSet.dataSetName, "", dataSet);
    }
</script>
```

To perform any actions after the report has been rendered using JavaScript code, simply define the name of the JavaScript function for the `onAfterRender` event. The function will receive the action type and the report itself as arguments. Example of displaying a message after the report is rendered:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.onAfterRender += 'afterRender'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**render.html**

```html

<script>
    function afterRender(args) {
        alert("The report rendering is completed.");
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).
