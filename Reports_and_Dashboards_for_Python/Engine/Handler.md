# Event Handler

The reporting tool, along with the viewer and report designer, can trigger events on the client side, transfer them to the Python server for further processing, and receive a response prepared. All actions are implemented in the event handler, eliminating the need for any additional functions to communicate between the client and server and transfer data. To handle a specific event, simply add the function name to the handler, and the specified function will be automatically called when the event occurs. Events can be called on both the JavaScript client side and the Python server side. If needed, you can add multiple functions of any type to the same event.

### Calling a JavaScript event on the client-side

To trigger a JavaScript event, you need to add the function name as a string to the event handler. The event arguments will include all the necessary data required for that specific event. A list of available arguments can be found in the [Reports Engine Events](Events.md) section.


An example of displaying a message with the number of pages of the received document after generating a report:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.onAfterRender += 'afterRender'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**report.html**

```html

<script>
    function afterRender(args) {
        let pagesCount = args.report.renderedPages.count;
        alert("The report is rendered, pages: " + pagesCount);
    }
</script>
```

In this example, you can obtain a JavaScript report object from the event arguments and read the number of pages in the document that was generated.


> **Information**
>
> More information about the available functions and parameters of the JavaScript reporting tool can be found in the documentation for the [Stimulsoft Reports.JS and Stimulsoft Dashboards.JS](Reports_JS) products.


### Calling a JavaScript Event on the Node.js server-side

When using the Node.js platform for working with reports, it is not possible to call a JavaScript function by name, as there is no HTML template involved. In this case, the event handler should contain the actual function as a string or code snippet. The event arguments will be stored in a predefined variable called args, which can be used within the event code.


Example of clearing the data dictionary in a template before building a report:


**app.py**

```python

from stimulsoft_reports.report import StiReport
from stimulsoft_reports.report.enums import StiEngineType

report = StiReport()
report.engine = StiEngineType.SERVER_NODE_JS
report.onBeforeRender += 'args.report.dictionary.clear();'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


> **Information**
>
> This same approach can be used when displaying the viewer or designer without an HTML template, where it’s not possible to predefine a JavaScript function in advance.


### Calling a Python event on the server-side

To trigger a Python event, you need to pass the function as a variable to the event handler. All necessary data for the specific event will be passed in the event arguments. A list of available arguments can be found in the [Report Engine Events](Events.md) section.


Example of adjusting the password in the connection string before requesting data:


**app.py**

```python

from stimulsoft_reports.events import StiDataEventArgs

def beginProcessData(args: StiDataEventArgs):
    args.connectionString = args.connectionString.replace('Pwd=;', 'Pwd=******;')

report = StiReport()
report.onBeginProcessData += beginProcessData
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```

In this example, all database connection parameters can be accessed and modified using the event arguments.


On the Python server side, it's possible to return a text message indicating the success or failure of the event. This message will be shown in the viewer or designer after the event completes. To display an error dialog, you should return one of the result types listed below:


| **Name** | **Description** |
| --- | --- |
| `StiResult.getError('Error message')` | Displays a dialog with a red icon and an exclamation mark, along with the specified error message. |
| `StiResult.getSuccess('Info message')` | Displays a dialog with a blue information icon and the specified informational message. |
| `False` | Displays a dialog with a red icon and a standard error message including the event name. |
| `'Info message'` | Equivalent to calling `StiResult.getSuccess('Info message')`. |
| `None` | Executes the event normally without displaying any messages. If an internal error occurs in the event handler, a relevant error message will be shown. |


Example of output of various messages from the event result:


**app.py**

from stimulsoft_reports import StiResultfrom stimulsoft_reports.designer import StiDesignerfrom stimulsoft_reports.events import StiReportEventArgsfrom stimulsoft_reports.report import StiReport
def saveReport(args: StiReportEventArgs):#StiResult.getError('An error occurred while saving.')#StiResult.getSuccess('The report was successfully saved.')return 'The report was successfully saved.'
designer = StiDesigner()designer.onSaveReport += saveReport

> **Information**
>
> When an error occurs in the event handler, such as a failure to connect to the database or an error processing a file, an internal message will be displayed regardless of whether a message is defined in the component event.


> **Information**
>
> The message dialog box will only appear when using the StiViewer or StiDesigner components. The reporting tool does not include visual forms, so event processing messages will be displayed in the browser console.

### Calling several identical events

It is possible to assign an unlimited number of functions to an event handler. They will be grouped by event type and executed sequentially in the order they were added. For example, you may want to modify the SQL query on the JavaScript client side and change the connection string on the Python server side:


An example of changing the SQL query on the JavaScript client-side, and the connection string on the PHP server side:


**app.py**

```python

from stimulsoft_reports.events import StiDataEventArgs
from stimulsoft_reports.report import StiReport

def beginProcessData(args: StiDataEventArgs):
    args.connectionString = args.connectionString.replace('Pwd=;', 'Pwd=;')

report = StiReport()
report.onBeginProcessData += beginProcessData
report.onBeginProcessData += 'beginProcessData'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**viewer.html**

```html

<script>
    function beginProcessData(args) {
        args.queryString = args.queryString.replace('TableName', 'Products')
    }
</script>
```


> **Information**
>
> Some events can only be triggered on the JavaScript client side and cannot be triggered on the Python server side. When adding a function to such an event, no error will occur, but the function will not be called. All supported options are listed in the section [Report Engine Events](Events.md).

### Encrypting data sent to the Python server

To prevent data theft by malicious actors, it is recommended to use the HTTPS protocol, which is sufficient in most cases. Additionally, by default, all transmitted data is passed through a special encoding algorithm and sent to the server in encrypted form. This helps protect sensitive information, such as login credentials in a connection string, from curious users interacting with your application.


However, if encryption is not required, for example, when debugging the application and needing to inspect the raw data, it is possible to disable encryption. To do this, simply set the `encryptData` property to `False` on the event handler. All data will then be sent in standard JSON format.


**app.py**

from stimulsoft_reports.report import StiReport
report = StiReport()report.handler.encryptData = False
