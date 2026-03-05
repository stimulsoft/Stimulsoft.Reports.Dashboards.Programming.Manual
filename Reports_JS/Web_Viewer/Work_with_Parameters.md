# Work with Parameters

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

We have a special settings panel to work with report parameters in the **HTML5 Viewer**. To add a parameter to the panel you need to define a variable in a report, requested by the user. When viewing a report in the viewer such a variable will be automatically added to the settings panel. It supports all types of report variables (normal variables, date and time, borders, lists, etc.).


![](../../images/topics/Reports_JS.Web_Viewer.Work_with_Parameters_1.png)


To work with reports with parameters, no additional viewer settings are required. If you need to perform some actions before applying the parameters, you can define a special **onInteraction** event. When using the parameters panel, the action type will be set to the **Variable** value.


**viewer.html**

```html
...
viewer.onInteraction = function (args) {
    if (args.action == "Variables") {
        var variables = args.variables;
    }
}
...
```


If you do not need to work with parameters, you can completely disable this feature. To do this, use the **showParametersButton** property in the **Toolbar** section of properties, which should be set to **false**.

**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.toolbar.showParametersButton = false;
...
```


> **Information**
>
> With such a viewer configuration, the options panel will not be displayed, even if the parameters are present in the displayed report.
