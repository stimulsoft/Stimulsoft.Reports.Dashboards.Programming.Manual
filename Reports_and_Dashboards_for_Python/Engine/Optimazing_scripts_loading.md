# Optimizing Scripts Loading

Due to the impressive functionality of the product, the scripts are quite large. When loading a web application for the first time, or when browser caching is disabled, loading may take some time, especially on a low-speed internet connection. We offer two options for solving this problem: using packaged scripts or employing partial functionality and loading only what is required. Simultaneous use of the specified options is permitted.

### Packed scripts

Packed scripts have the same structure as regular scripts but end with `*.pack.js` in the file name. Such scripts contain a block of packed data in the form of a JavaScript variable and a compact unpacker. When loading all scripts, the unpacker automatically unpacks all downloaded data and launches the prepared script for execution. Unpacking takes some time, but under certain circumstances - such as with a slow internet connection - this time is much less than the loading speed of regular scripts.


To use packaged scripts, all you should do is set the `javascript.usePacked` property of the report object to `True`, for example:


**app.py**

```python

report = StiReport()
report.javascript.usePacked = True
```

### Partial loading of scripts

When deploying the reporting tool, by default only one file with scripts, `stimulsoft.reports.js`, is loaded. It contains all the functionality for building and exporting reports. If you only need some of the capabilities to generate reports, you can download only the required parts of the generator that contain a specific set of capabilities. For example, if your reports do not use maps, you don't have to download them. This will speed up the loading of the web project and reduce memory consumption by the browser.


> **Information**
>
> This feature is implemented only for the report engine; the viewer and designer cannot be divided into parts; their scripts will be loaded entirely in one block.

To use partial loading of scripts, just set the necessary options for the `javascript` property of the report object:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()

report.javascript.reportsChart = True
report.javascript.reportsExport = True
report.javascript.reportsImportXlsx = True
report.javascript.reportsMaps = False
report.javascript.blocklyEditor = False
```

Each option controls the loading of a script containing specific functionality. This table presents the entire set of scripts that can be loaded separately:


| **Name** | **Description** |
| --- | --- |
| `javascript.reportsExport` | Contains algorithms for exporting the generated report to various formats - PDF, HTML, Excel, RichText, and others. |
| `javascript.reportsChart` | Contains components for working with all types of charts in a report. |
| `javascript.reportsMaps` | Contains components for working with regional and online maps. |
| `javascript.blocklyEditor` | Contains the Blockly visual editor for creating event scripts in the report. The event handler itself is built into the reporting engine. |
| `javascript.reportsImportXlsx` | Contains algorithms for working with Excel data sources. |


> **Information**
>
> The report viewer and report designer components also have a `javascript` property, with which you can control the configuration of scripts the way described above.
