# Working with Report Variables

The viewer includes support for a special parameters panel for working with report variables. To add a parameter to the panel, a variable that requires user input must be defined in the report. When viewing the report in the viewer, this variable will automatically be added to the parameters panel. All types of report variables are supported (standard variables, date and time, range, lists, etc.).


### Values of variables on the parameters panel

A special `onInteraction` event is provided for performing actions before applying the parameters, which will be triggered by any interactive actions in the viewer. The event arguments will include the action type, the report object, and a collection of variables and their values on the parameters panel. In this case, the action type will be `Variables`.  A detailed description of the available argument values can be found in the [Viewer Events](Events.md) section.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.onInteraction += 'interaction'
```


**viewer.html**

```html

<script>
    function interaction(args) {
        if (args.action == "Variables") {
            let variables = args.variables;
        }
    }
</script>
```

The variable collection is an object that contains all the variables from the parameters panel. It’s allowed to change the values of the variables, but the type of the new value must match the type of the variable being modified.


**viewer.html**

```html

<script>
    let variables = {
        VariableString: "Text value",
        VariableInt: 20
    }
</script>
```

Direct access to the variable values on the parameters panel from the Python server side isn’t provided, the event works only on the JavaScript client-side.

### Parameters panel settings

If working with variables in the viewer is not required, this feature can be completely disabled. To do so, set the `showParametersButton` property to `False`.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.toolbar.showParametersButton = False
```


> **Inforrmation**
>
> With this viewer configuration, the parameters panel will not be displayed, even if parameters are present in the report being viewed.

### Variable values when building a report

If it is necessary to control all report variables, a special `onPrepareVariables` event is available, which will be triggered before the report is generated.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.events import StiReportEventArgs

def prepareVariables(args: StiVariablesEventArgs):
    variables = args.variables

viewer = StiViewer()
viewer.onPrepareVariables += onPrepareVariables
viewer.onPrepareVariables += 'onPrepareVariables'
```


**viewer.html**

```html

<script>
    function prepareVariables(args) {
        let variables = args.variables;
    }
</script>
```

A detailed description of this event can be found in the [Working with Report Variables](../Engine/Using_Variables.md) section of the report generator documentation.
