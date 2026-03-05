# Preview

The designer has a preview mode for the edited report. To access it, simply navigate to the appropriate tab in the designer window. The report template will be rendered and displayed in the built-in viewer.

### Preview events

Before previewing the report, you have the opportunity to carry out any necessary actions. For this purpose, there is a special event called `onPreviewReport`, which will be triggered before the report is viewed. The event arguments will include the report intended for preview.


Within an event on the Python server side, modifications to the report or its parameters are permitted.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner
from stimulsoft_reports.events import StiReportEventArgs

def previewReport(args: StiReportEventArgs):
    args.report['ReportDescription'] = 'This is a report description from the Python server-side.'

designer = StiDesigner()
designer.onPreviewReport += previewReport
```

All functionalities of the reporting tool are accessible in the client-side JavaScript event. For example, you can connect data for a report.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner

designer = StiDesigner()
designer.onPreviewReport += 'previewReport'
```


**designer.html**

```html

<script>
    function previewReport(args) {
        let dataSet = new Stimulsoft.System.Data.DataSet("Demo");
        dataSet.readJsonFile("/static/data/Demo.json");
        
        let report = args.report;
        report.regData(dataSet.dataSetName, "", dataSet);
    }
</script>
```

You can find a list of available built-in viewer events and descriptions of use cases in the [Viewer Events](../Web_Viewer/Events.md) section.

### Additional features

The report preview window in the designer is a fully interactive viewer that can print and export the report, and supports working with report parameters. All available interactive actions are supported, such as dynamic sorting, drill-down, and collapsing. You do not need any additional settings in the report designer to use these features.
