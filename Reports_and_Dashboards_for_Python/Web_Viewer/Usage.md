# Usage

> **Examples**
>
> The complete code sample can be found on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).

To use the viewer, simply install  [stimulsoft-reports](https://pypi.org/project/stimulsoft-reports) or [stimulsoft-dashboards](https://pypi.org/project/stimulsoft-dashboards) package using the package manager by running the following command:


**console**

python -m pip install stimulsoft-reports


**console**

python -m pip install stimulsoft-dashboards

The latest available version of the product will be installed in the current workspace, after which you can use the classes and functions for working with reports and dashboards.


> **Information**
>
> The examples in the documentation use the **Flask** framework, as it’s one of the most popular and easy-to-understand frameworks. You can use any web framework, as all classes and functions for working with the components are universal.

To add a viewer to a web project, the `StiViewer` class is intended. Using this class, you can create a viewer object, set the necessary settings, handle a request and return its result, and get the prepared JavaScript and HTML code for the component. Here is an example of displaying the viewer on an HTML page:


**app.py**

```python

from flask import Flask, render_template, url_for, request
from stimulsoft_reports.viewer import StiViewer

app = Flask(__name__)

@app.route('/viewer', methods = ['GET', 'POST'])
def viewer():
    viewer = StiViewer()
    viewer.options.appearance.fullScreenMode = True

    if viewer.processRequest(request):
        return viewer.getFrameworkResponse()

    js = viewer.javascript.getHtml()
    html = viewer.getHtml()
    return render_template('viewer.html', viewerJavaScript = js, viewerHtml = html)
```


**viewer.html**

```html

<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Showing a Report in the Viewer</title>
    
    {{ viewerJavaScript|safe }}
</head>

<body>
    {{ viewerHtml|safe }}
</body>

</html>
```

In this example, an instance of the `StiViewer` object is created, and the necessary settings are configured.


The special component function `processRequest(request)` processes the current request. If the function returns `True`, it means the request was successfully processed, and the result of its execution should be returned. More details about this are provided in the [Event Handler](../Engine/Handler.md) section.


Next, it’s necessary to generate the prepared JavaScript and HTML code required for the viewer to work. The `viewer.javascript.getHtml()` function generates the HTML code to connect the necessary scripts and resources, and the `viewer.getHtml()` function generates the HTML code for the component itself. The generated code is passed as parameters to the HTML template viewer.html and displayed in the designated locations.


> **Information**
>
> Our products [Stimulsoft Reports.PYTHON](https://www.stimulsoft.com/en/products/reports-python) and [Stimulsoft Dashboards.PYTHON](https://www.stimulsoft.com/en/products/dashboards-python) don’t have a native report generator core in Python. Report generation and export are performed on the client-side using JavaScript code. When using Python code to work with the components, you need to call the `getHtml()` function, which will return all the necessary JavaScript and HTML code for the report generator and components to work.

A simplified viewer deployment is available without using an HTML page template. For example, the same example can be implemented using only Python code:


**app.py**

```python

from flask import Flask, url_for, request
from stimulsoft_reports.viewer import StiViewer

app = Flask(__name__)

@app.route('/viewer', methods = ['GET', 'POST'])
def viewer():
    viewer = StiViewer()
    viewer.options.appearance.fullScreenMode = True

    if viewer.processRequest(request):
        return viewer.getFrameworkResponse()

    # Here is the code for working with the report

    return viewer.getFrameworkResponse()
```

In this case, after calling the event handler and performing actions with the report, the final result of the request is returned immediately. That is, the viewer will return a fully prepared HTML page with all the necessary scripts and code. Other methods of operation are also available, which are described in more detail in the [Event Handler](../Engine/Handler.md) section.


> **Information**
>
> In most cases, it is sufficient to use only Python code to work with the product, which allows interaction with all the main features of the components. For detailed product customization and using all the features of the JS generator, you need to use JavaScript code. The method of deploying the product using only JavaScript code is described in the section  [Reports and Dashboards for JS](../../Reports_JS/index.md), in this case, Python code is only required to [connect data adapters](../Engine/Connecting_SQL_Data.md).

To generate a response, the `getFrameworkResponse()` function is used, which returns a ready object suitable for the currently used web framework. The current framework is determined at the time of request processing. Our components support working with popular frameworks like **Django**, **Flask**, and **Tornado**. To process the request and generate a response in web projects that don’t use these frameworks, you need to pass the current GET and POST data to the request processing function, and to generate a response, use the `getResponse()` function, which will return all the necessary data. For example, you can implement the viewer event handling in the following way:


**app.py**

```python

from flask import Flask, make_response, render_template, url_for, request
from stimulsoft_reports.viewer import StiViewer

app = Flask(__name__)

@app.route('/viewer', methods = ['GET', 'POST'])
def viewer():
    viewer = StiViewer()
    viewer.options.appearance.fullScreenMode = True

    query = request.args.to_dict()
    body = request.get_data(False)
    if viewer.processRequest(None, query, body):
        viewerResponse = viewer.getResponse()
        response = make_response(viewerResponse.data)
        response.mimetype = viewerResponse.mimetype
        response.headers.add('Access-Control-Allow-Origin', request.origin)
        return response

    js = viewer.javascript.getHtml()
    html = viewer.getHtml()
    return render_template('viewer.html', viewerJavaScript = js, viewerHtml = html)
```
