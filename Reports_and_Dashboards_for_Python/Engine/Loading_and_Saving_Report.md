# Loading and Saving Reports

> **Information**
>
> The Stimulsoft MRT and MDC format file is a description of reports with XML or JSON markup. You can use MRT and MDC files created in other Stimulsoft report designers.


### Loading report

To load a report using Python code, you can use one of the functions listed below on the `StiReport` object. Each of the functions takes as input either the name of the report file or the report itself as a string.


| **Name** | **Description** |
| --- | --- |
| `loadFile(filePath: str, load: bool = False)` | Loads a report from an MRT file on the client side, with the file path specified in the function arguments. If the `load` parameter is set to `True`, the report file will be loaded on the server side and then transferred to the client side as a `Base64` encoded string. |
| `load(data: str, fileName: str = 'Report')` | Loads a report from an XML or JSON string and sends it to the client side as a `Base64`-encoded string. The `fileName` parameter specifies the file name to be used for saving and exporting the report in the future. |
| `loadPacked(data: str, fileName: str = 'Report')` | Transmits a report to the client side as a `Base64`-encoded string specified in the `data` parameter. The `fileName` parameter specifies the file name that will be used for subsequent saving and exporting of the report. |
| `loadDocumentFile(filePath: str, load: bool = False)` | Loads a document from an MDC file on the client side, with the path specified in the function parameters. If the `load` parameter is set to `True`, the document file will be loaded on the server side and transferred to the client side as a `Base64`-encoded string. |
| `loadDocument(data: str, fileName: str = 'Report')` | Loads a document from an XML or JSON string and transfers it to the client side as a `Base64`-encoded string. The `fileName` parameter specifies the file name to be used for subsequent saving and exporting of the report. |
| `loadPackedDocument(data: str, fileName: str = 'Report')` | Transfers the document to the client side as a `Base64`-encoded string specified in the `data` parameter. The `fileName` parameter specifies the file name to be used for subsequent saving and exporting of the report. |

An example of loading a report from a file on the server-side from a private directory and transferring it to the client side as a packed string for subsequent construction:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'), True)
report.render()
```

### Saving the report

Since the reporting tool for Python is based on a JavaScript platform and renders and exports reports on the client side, you should use events and JavaScript functions to save a report or document template. You can find more details in the section [Reporting tool events](Events.md).


An example of saving a constructed report as a string for later use:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.onAfterRender += 'afterRender'
report.loadFile(url_for('private', filename='reports/SimpleList.mrt'), True)
report.render()
```


**report.html**

```html

<script>
    function afterRender(args) {
        let json = args.report.saveDocumentToJsonString();
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


In the server-side report generation mode, one of the following methods is used to save the report:


| **Name** | **Description** |
| --- | --- |
| `saveDocument(filePath: str = None)` | Saves the built report as an MDC file at the path specified in the function arguments. If the `$filePath` parameter isn’t specified, the method will return the report as a JSON string instead of saving the file. |
| `savePackedDocument(filePath: str = None)` | Saves the built report as a packed MDZ file at the path specified in the function arguments. If the `$filePath` parameter isn’t specified, the method will return the report as a packed `Base64` string instead of saving the file. |

For example, you need to save the rendered report as a file on the server side:


**app.py**

```python

from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiEngineType

report = StiReport()
report.engine = StiEngineType.SERVER_NODE_JS
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'), True)
report.render()
report.saveDocument(url_for('static', filename='reports/SimpleList.mdc'))
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


> **Information**
>
> [Stimulsoft Reports.PYTHON](https://www.stimulsoft.com/en/products/reports-python) and [Stimulsoft Dashboards.PYTHON](https://www.stimulsoft.com/en/products/dashboards-python) support saving MRT files only in JSON format. MRT files in XML format are only supported in download mode and will be automatically converted to JSON format upon saving.
>
>
> Because dashboards always require data, they cannot be saved as documents. [Stimulsoft Dashboards.PYTHON](https://www.stimulsoft.com/en/products/dashboards-python) supports saving dashboards only as templates.
>
>
> When saving a document from the viewer menu, the file is saved in JSON format and uses the extension MDC for a standard document, MDZ for a packed document, and MDX for an encrypted document.
