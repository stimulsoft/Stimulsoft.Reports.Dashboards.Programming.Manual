# Usage

To use the reporting tool, just install [stimulsoft-reports](https://pypi.org/project/stimulsoft-reports) or [stimulsoft-dashboards](https://pypi.org/project/stimulsoft-dashboards) package via a package manager by executing one of the following commands:


| **console** |
| --- |
| python -m pip install stimulsoft-reports |


| **console** |
| --- |
| python -m pip install stimulsoft-dashboards |


> **Information**
>
> For Linux systems, an additional package for working with ODBC may be required. This can be installed, for example, by running the following command:
>
>
> `sudo apt-get install unixodbc`.

The latest available version of the reporting tool will be installed in the current workspace, after which you can use classes and functions for working with reports.


By default, a minimal set of data drivers is installed. The necessary drivers can be additionally installed manually, or use the command to install all available drivers:


| **console** |
| --- |
| python -m pip install stimulsoft-reports[ext] |


| **console** |
| --- |
| python -m pip install stimulsoft-dashboards[ext] |


> **Information**
>
> The code examples use the Flask framework, as it is one of the most popular and easiest to understand. However, any web framework can be used, since all classes and functions for working with the report generator are universal.

The class for working with the report generator is StiReport. This class allows you to load report templates or documents, build and export reports, process requests, and manage report generator events.


For example, to load a report from a file and build it, then display a message in the browser window:


**app.py**

```python

from flask import Flask, render_template, url_for, request
from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiExportFormat

app = Flask(__name__)

@app.route('/report', methods = ['GET', 'POST'])
def report():
    report = StiReport()
    if report.processRequest(request):
        return report.getFrameworkResponse()

    report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
    report.render()
    report.exportDocument(StiExportFormat.HTML)

    js = report.javascript.getHtml()
    html = report.getHtml()
    return render_template('report.html', reportJavaScript = js, reportHtml = html)
```


**index.html**

```html

<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Render and Export a Report</title>

    {{ reportJavaScript|safe }}
</head>

<body>
    {{ reportHtml|safe }}
</body>

</html>
```


The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


In this example, the following steps are performed sequentially:

- a new instance of the `StiReport` object is created;
- required event handlers are added;
- the current request is processed;
- the report template `SimpleList.mrt` is loaded from the static files directory;
- the report build command is executed;
- JavaScript event code is added to the HTML template, and the necessary JavaScript and HTML code for the component is rendered;


The `report.processRequest(request)` method processes the current request and returns the result. If processing is successful, the result should be returned instead of the page template. More details are provided in the Event Handler [Event Handler](Handler.md)  section.


The method `report.javascript.getHtml()` generates the required JavaScript code for connecting the component scripts. The `report.getHtml()` method generates the combined JavaScript and HTML code for the component. The generated HTML is passed to the `report.html` template and rendered in the appropriate location.


Our products [Stimulsoft Reports.PYTHON](https://www.stimulsoft.com/en/products/reports-python) and [Stimulsoft Dashboards.PYTHON](https://www.stimulsoft.com/en/products/dashboards-python) don't have a native Python report generation engine. Report building and export are performed using JavaScript on the client-side, or on the server-side via the Node.js platform. Therefore, when using Python code to work with components, you must call one of the special methods that injects the necessary JavaScript and HTML code into the web page for rendering the visual report component.


| **Name** | **Description** |
| --- | --- |
| `getHtml(mode = StiHtmlMode.HtmlScripts)` | Returns the JavaScript and HTML code required for the component to function, including all necessary operations on the report. The `mode` parameter determines the returned format: ·    `StiHtmlMode.Scripts` – only the JavaScript code to embed in a &lt;script&gt;&lt;/script&gt; a complete HTML page; ·    `StiHtmlMode.HtmlScripts` – combined JavaScript and HTML code to embed in an HTML element; ·    `StiHtmlMode.HtmlPage` – a complete HTML page. **Note:** The `getHtml()` method of component objects, for example `report.javascript,` doesn't accept parameters, as it has only one output format. |
| `renderHtml(elementId: str = None)` | Renders the JavaScript and HTML code required for the component. The `elementId` parameter specifies the HTML element where the component will be rendered. By default, it renders at the current position on the page. |
| `printHtml()` | Renders a fully prepared HTML page with all necessary scripts for the component. The current HTML template is ignored. This mode is ideal for full-screen report viewing or editing. |

Thus, the above methods allow you to render the component in various ways depending on your needs. Example of simplified component rendering without using an HTML page template:


**app.py**

from flask import Flask, url_for, requestfrom stimulsoft_reports.report import StiReport
app = Flask(__name__)
@app.route('/report', methods = ['GET', 'POST'])def report():report = StiReport()report.onAfterRender += "alert('Done!');"if report.processRequest(request):return report.getFrameworkResponse()
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))report.render()
return report.getFrameworkResponse()


**Information**


When using the Node.js platform to build a report on the Python server side, the specified methods will be called automatically within the handler, and their explicit use is not required.

### Framework support

Currently, built-in support is implemented for three popular Python frameworks: **Flask**, **Django**, and **Tornado**. Universal functions are also available for working with any other frameworks. **Flask** is used in the code examples as one of the most popular and beginner-friendly frameworks. Deployment for Flask was covered earlier. Below are examples of the same code adapted for the other supported frameworks. All of them are very similar and differ only in the specific functions used for each framework.


**Django**


**app.py**

```python

from django.shortcuts import render
from django.templatetags.static import static
from stimulsoft_reports.report import StiReport

def report(request):
    report = StiReport()
    report.onAfterRender += 'afterRender'

    if report.processRequest(request):
        return report.getFrameworkResponse()

    report.loadFile(static('reports/SimpleList.mrt'))
    report.render()

    js = report.javascript.getHtml()
    html = report.getHtml()
    return render(request, 'report.html', {'reportJavaScript': js, 'reportHtml': html})
```


**report.html**

```html

<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Render and Export a Report</title>

    {{ reportJavaScript|safe }}

        <script type="text/javascript">
        function afterRender() {
        alert('Done!');
        }
   </script>
</head>

<body>
    {{ reportHtml|safe }}
</body>

</html>
```

**Tornado**


**app.py**

```python

import asyncio, os
from tornado.web import Application, RequestHandler, url
from stimulsoft_reports.report import StiReport

class ReportHandler(RequestHandler):
    def get(self):
        report = StiReport()
        report.onAfterRender += 'afterRender'

        if report.processRequest(request):
            return report.getFrameworkResponse(self)

        report.loadFile(self.static_url('reports/SimpleList.mrt'))
        report.render()

        js = report.javascript.getHtml()
        html = report.getHtml()
        self.render('report.html', reportJavaScript = js, reportHtml = html)

    def post(self):
        handler = StiHandler()
        if handler.processRequest(self.request):
            return handler.getFrameworkResponse(self)
```


**report.html**

```html

<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Render and Export a Report</title>
    
    {% raw reportJavaScript %}
        <script type="text/javascript">
        function afterRender() {
        alert('Done!');
        }
   </script>
</head>

<body>
    {% raw reportHtml %}
</body>

</html>
```

### Universal functions

When using any other framework, instead of the `getFrameworkResponse()` method, you should use the `getResponse()` method, which returns a `StiResponse` object containing all the necessary parameters for forming the response:


**app.py**

```python

from stimulsoft_reports.report import StiReport

def report():
    report = StiReport()
    report.onAfterRender += 'afterRender'
    query = 'query string'
    body = 'post data'
    if report.processRequest(None, query, body):
        response = report.getResponse()
        data = response.data
        contentType = response.contentType
        mimetype = response.mimetype

    report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
    report.render()

    js = report.javascript.getHtml()
    html = report.getHtml()
```


> **Information**
>
> In most cases, to work with the product, you should use only Python code, which provides interaction with all the main features. To configure the product more precisely and utilize all the capabilities of the JS reporting software, you must use JavaScript code. The option to deploy a product using only JavaScript code is described in the [Reports and Dashboards for JS](../../Reports_JS/index.md)section. In this case, the use of Python code is required only to [connect data adapters](Connecting_SQL_Data.md).

Various deployment and optimization options are discussed in the section [Optimizing scripts loading](Optimazing_scripts_loading.md).
