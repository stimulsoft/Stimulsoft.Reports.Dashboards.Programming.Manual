# Deployment

> **Examples**
>
> The complete code sample can be found on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).

To use the designer, simply install the  [stimulsoft-reports](https://pypi.org/project/stimulsoft-reports) or [stimulsoft-dashboards](https://pypi.org/project/stimulsoft-dashboards) package using the package manager by executing the following command:

| **console** |
| --- |
| python -m pip install stimulsoft-reports |


| **console** |
| --- |
| python -m pip install stimulsoft-dashboards |

The latest available version of the product will be installed in the current workspace, after which you can use the classes and functions for working with reports and dashboards.


> **Information**
>
> The code examples in the documentation use the **Flask** framework, as it is one of the most popular and easy-to-understand frameworks. You can use any web framework; all classes and functions for working with components are universal.

To add the designer to a web project, the `StiDesigner` class is used. This class allows you to create a designer object, set the necessary settings, handle requests and return the result, and obtain the prepared JavaScript and HTML code of the component. Here is an example of displaying the designer on an HTML page:


**app.py**

```python

from flask import Flask, render_template, url_for, request
from stimulsoft_reports.designer import StiDesigner

app = Flask(__name__)

@app.route('/designer', methods = ['GET', 'POST'])
def designer():
    designer = StiDesigner()
    designer.options.appearance.fullScreenMode = True

    if designer.processRequest(request):
        return designer.getFrameworkResponse()

    js = designer.javascript.getHtml()
    html = designer.getHtml()
    return render_template('designer.html', designerJavaScript = js, designerHtml = html)
```


**designer.html**

```html

<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Editing a Report Template in the Designer</title>
    
    {{ designerJavaScript|safe }}
</head>

<body>
    {{ designerHtml|safe }}
</body>

</html>
```

In this example, an instance of the `StiDesigner` object is created, and the necessary settings are applied.


The special component function `processRequest(request)` processes the current request. If the function returns `True`, the request was successfully processed, and you need to return the result of its execution. More details about this can be found in the [Event Handler](../Engine/Handler.md) section.


Next, you need to generate the prepared JavaScript and HTML code required for the designer to work. The `designer.javascript.getHtml()` function generates the HTML code to include the necessary scripts and resources, and the `designer.getHtml()` function generates the HTML code of the component itself. The generated code is passed as parameters to the HTML template designer.html and displayed in the specified places.


> **Information**
>
> Our products, [Stimulsoft Reports.PYTHON](https://www.stimulsoft.com/en/products/reports-python) and [Stimulsoft Dashboards.PYTHON](https://www.stimulsoft.com/en/products/dashboards-python) don’t have a native report generator core in Python; report building and exporting are performed on the client side using JavaScript code. When using Python code to work with components, you need to call the `getHtml()` function, which will return all the necessary JavaScript and HTML code for the report generator and components.

There is a simplified deployment of the designer without using an HTML page template. For example, the same example can be implemented using only Python code:


**app.py**

```python

from flask import Flask, url_for, request
from stimulsoft_reports.designer import StiDesigner

app = Flask(__name__)

@app.route('/designer', methods = ['GET', 'POST'])
def designer():
    designer = StiDesigner()
    designer.options.appearance.fullScreenMode = True

    if designer.processRequest(request):
        return designer.getFrameworkResponse()

    # Here is the code for working with the report

    return designer.getFrameworkResponse()
```

In this case, after calling the event handler and performing actions with the report, the final result of the request is immediately returned. That is, the designer will return a fully prepared HTML page with all the necessary scripts and code.


> **Information**
>
> In most cases, using the product requires only Python code, which interacts with all the main capabilities of the components. For detailed product configuration and access to all the features of the JS generator, JavaScript code is needed. The deployment option using only JavaScript code is described in the [Reports and Dashboards for JS](../../Reports_JS/index.md) section, in this case, Python code is only required for [connecting SQL data adapters](../Engine/Connecting_SQL_Data.md).

To form the response, the `getFrameworkResponse()` function is used, which returns a ready-made object suitable for the currently used web framework. The current framework is determined at the time of request processing. Our components support popular frameworks like **Django**, **Flask**, and **Tornado**. For handling requests and forming responses in web projects that do not use these frameworks, you need to pass the current GET and POST data to the request processing function and use the `getResponse()` function to generate the response, which will return all the necessary data. For example, handling designer events can be implemented in the following way:


**app.py**

from flask import Flask, make_response, render_template, url_for, requestfrom stimulsoft_reports.designer import StiDesigner
app = Flask(__name__)
@app.route('/designer', methods = ['GET', 'POST'])def designer():designer = StiDesigner()designer.options.appearance.fullScreenMode = True
query = request.args.to_dict()body = request.get_data(False)if designer.processRequest(None, query, body):designerResponse = designer.getResponse()response = make_response(designerResponse.data)response.mimetype = designerResponse.mimetyperesponse.headers.add('Access-Control-Allow-Origin', request.origin)return response
js = designer.javascript.getHtml()html = designer.getHtml()return render_template('designer.html', designerJavaScript = js, designerHtml = html)
