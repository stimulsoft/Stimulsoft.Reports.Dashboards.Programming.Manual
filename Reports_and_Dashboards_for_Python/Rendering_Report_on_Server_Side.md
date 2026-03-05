# Rendering a Report on Server Side

To build a report on the server-side, the universal Node.js platform is used. This platform executes the necessary block of JavaScript code and returns the prepared result.


**Deploying the Node.js platform**

Before using the report generator on the server-side, you need to install the Node.js platform and configure it. This can be done separately by following the Node.js installation instructions for a specific operating system from the [official platform website](https://nodejs.org/en), or automatically using a special deployment function.
If the platform is already installed, it will be detected automatically, no settings are required. It is possible to specify the path to the directory of the platform executable files, if necessary. You can also specify the path to the working directory in which the necessary Node.js packages will be installed.


**app.py**

```python

from stimulsoft_reports import StiNodeJs

nodejs = StiNodeJs()

# nodejs.binDirectory = 'C:\\Program Files\\nodejs'
# nodejs.binDirectory = '/usr/bin/nodejs'

# nodejs.workingDirectory = ''
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


If the platform and packages aren’t installed, special methods can be used to install them. These methods need to be called only once: the first method installs the Node.js platform itself, and the second method installs or updates all necessary packages to the latest version:


**app.py**

```python
...

result = nodejs.installNodeJS()
if result:
    result = nodejs.updatePackages()

message = 'The installation was successful.' if result else nodejs.error
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


The platform and packages will be installed in the specified working directory.


### Building a report

To switch the report generator to server-side operation, you need to set the report's engine property to `StiEngineType::ServerNodeJS`. The rest of the events and methods for working with the report are exactly the same as when building a report on the client-side.
After calling the `render()` method on the report object, the built report can be saved using the `saveDocument()` or `savePackedDocument()` methods, as described in the [Loading and Saving a Report](../Reports_and_Dashboards_for_PHP/Engine/Loading_and_Saving_Report.md) section. Additionally, after building the report, it can be exported to one of many formats using the `exportDocument()` method, as described in the [Exporting a Report from Code](../Reports_and_Dashboards_for_PHP/Engine/Export_from_Code.md) section.
Example of loading and building a report template, and subsequently saving the built report to a file on the server-side:


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

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


Any errors that occur when working with Node.js packages, as well as when building and exporting a report on the server-side, can be read in the `report->nodejs->error` and `report->nodejs->errorStack` properties. These properties will contain the last error in the queue:


**app.py**

```python

from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiEngineType

report = StiReport()
report.engine = StiEngineType.SERVER_NODE_JS
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'), True)
result = report.render()
if not result:
    # The main text of the error as a string.
    error = report.nodejs.error
    # The full error text as an array of strings.
    errorStack = report.nodejs.errorStack
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).
