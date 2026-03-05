# Working with Report Variables

The report generator allows you to use variables in expressions, queries, filters, and other report elements. It also supports previewing and modifying variable values from code before building the report.


### Report template variable values

The report generator provides easy access to template variables through the report’s data dictionary. You can do this by defining the `onBeforeRender` event on the report object. On the client side, the report object will be passed as a JavaScript object in the event arguments. Detailed information about the available event arguments is provided in the [Report Engine Events](Events.md) section.


To access a report variable, use the `getByName()` JavaScript function on the variables collection within the report's data dictionary. To change a variable's value, simply assign it to the `value` property — there is no need to manually convert the type, as type conversion will be handled automatically.


Example of changing the string and integer values ​​of selected variables on the client JavaScript side:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.onBeforeRender += 'beforeRender'
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
```


**report.html**

```html

<script>
    function beforeRender(args) {
        let report = args.report;
        
        let variableString = report.dictionary.variables.getByName("VariableString");
        variableString.value = "Text value";
        
        let variableInt = report.dictionary.variables.getByName("VariableInt");
        variableInt.value = "20";
    }
</script>
```

Direct access to report variables from the Python server side is not supported.


> **Information**
>
> The variable values are modified in the report template itself and will be saved in the file upon saving the report. If you want to change variable values without altering the template, use the `onPrepareVariables` event, which is triggered when variable values are prepared before report generation.

### Variable values ​​when building a report

**The report generator allows access to variables before the report is built by defining the onPrepareVariables event on the report object. The event arguments contain a collection of report variables, along with their types and values. If a variable is initialized as an expression, the evaluated result will be included in the collection. A detailed description of the available property values â€‹â€‹passed in event arguments can be found in the Report Engine Events section.**


**In the JavaScript client-side event, the variable collection is an array of objects, each containing the variable name, type, and value. You can modify the variable values, but the new value must match the type of the original variable.**


**report.html**

```html

<script>
    function prepareVariables(args) {       
        args.variables = [{
            name: "VariableString",
            type: "String",
            value: "Text value"
        },
        {
            name: "VariableInt",
            type: "Int32",
            value: 20
        }];
    }
</script>
```

Example of modifying a variable value on the JavaScript client-side:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.onPrepareVariables += 'prepareVariables'
report.loadFile(url_for('static', filename='reports/Variables.mrt'))
report.render()
```

On the Python server-side, the collection is represented as a dictionary of `StiVariable` objects. Each object stores the variable name, type, and value. The dictionary key matches the report variable name.


**report.html**


<script>

function prepareVariables(args) {

let variables = args.variables;


variables.find(item => item.name == "VariableString").value = "Text value";

variables.find(item => item.name == "VariableInt").value = 20;
}
</script>

You can also modify variable values on the Python server side, ensuring the type of the new value matches the variable type. Additionally, you can create new report variables if needed. Only modified or newly created variables will be sent to the client.


Example of modifying a variable on the PHP server-side:


**app.py**

from stimulsoft_reports.report import StiReportfrom stimulsoft_reports.events import StiVariablesEventArgs
def prepareVariables(args: StiVariablesEventArgs):args.variables['VariableString'].value = 'Text value'args.variables['VariableInt'].value = 20
report = StiReport()report.onPrepareVariables += prepareVariablesreport.loadFile(url_for('static', filename='reports/Variables.mrt'))report.render()

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


**app.py**

from stimulsoft_reports.events import StiVariablesEventArgs
def prepareVariables(args: StiVariablesEventArgs):args.variables['VariableString'].value = 'Value from Server-Side'args.variables['VariableInt'].value = 123args.variables['VariableDecimal'].value = 123.456

`DateTime` variables are passed as a string value in the format `"YYYY-MM-dd HH-mm-ss"`, or as a `datetime` object, for example:


**app.py**

```python

from datetime import datetime
from stimulsoft_reports.events import StiVariablesEventArgs

def prepareVariables(args: StiVariablesEventArgs):
    args.variables['VariableDateTime'].value = '2021-03-20 22:00:00'
    args.variables['VariableDateTime'].value = datetime.today()
```

To change the value of a `Range` variable, you must use the nested values `​​value['from']` and `value['to']` of the selected variable in the collection. The format of each of the two values ​​is the same as for a simple variable, for example:


**app.py**

```python

from stimulsoft_reports.events import StiVariablesEventArgs

def prepareVariables(args: StiVariablesEventArgs):
    args.variables['VariableStringRange'].value['from'] = 'Aaa'
    args.variables['VariableStringRange'].value['to'] = 'Zzz'
```

To change the value of a `List` type variable, you need to access the list value by its index. It is possible to set the values ​​of the entire list at once as a prepared array, for example:


**app.py**

```python

from stimulsoft_reports.events import StiVariablesEventArgs

def prepareVariables(args: StiVariablesEventArgs):
    args.variables['VariableStringList'].value[0] = 'Test'
    args.variables['VariableIntList'].value = [1, 22, 333]
```

To create a new variable that is not defined in the report, you must add a new `StiVariable` type object to the variable dictionary using the new variable name. After that, the variable can be used to build the report, i.e. the variable will not be saved in the report template.


**app.py**

```python

from stimulsoft_reports.report import StiVariable
from stimulsoft_reports.report.enums import StiVariableType

def prepareVariables(args: StiVariablesEventArgs):
    args.variables['NewVarInt'] = StiVariable('NewVarInt', StiVariableType.INT, 10)
```

After the `onPrepareVariables` event is processed, a new collection will be sent to the client containing only the variables whose values were changed, as well as any newly created variables.


> **Information**
>
> If a variable is used in an SQL query as an expression — that is, enclosed in curly braces like {VariableName} — its value will not be automatically escaped. You are responsible for ensuring the safety of the input values. Alternatively, you can use the variable as a query parameter, such as @VariableName. A detailed explanation of how parameters work can be found in the [Connecting SQL Data Adapters](Connecting_SQL_Data.md) section.

### Report variables passed in the URL request

The report generator supports automatically assigning values to variables passed through a URL request. To enable this feature, you must set the `passQueryParametersToReport` property to `True` in the event handler:


**app.py**

```python

@app.route('/report', methods = ['GET', 'POST'])
def report():
    report = StiReport()
    report.handler.passQueryParametersToReport = True
    if report.processRequest(request):
        return report.getFrameworkResponse()
```

All other actions will be handled automatically by the report generator. If the variable exists in the report, its value will be updated with the value from the URL. If the variable does not exist, it will be created temporarily for report generation, meaning it will not be saved in the report template. Variable names passed in the URL are case-insensitive.


> **Information**
>
> All variable values will be assigned before the `onPrepareVariables` event is triggered. This allows you to additionally control or adjust the values during this event, if necessary.
