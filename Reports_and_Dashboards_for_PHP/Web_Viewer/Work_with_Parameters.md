# Work with Report Variables

The viewer includes a dedicated parameters panel for handling report variables. To add a parameter to this panel, you need to define a variable in the report that will be requested from the user. When viewing the report in the viewer, such a variable will automatically appear on the parameters panel. All types of report variables are supported, including standard variables, date and time, ranges, lists, and more.


**Managing variables on the parameters panel**

To perform actions before applying parameters, there’s a special event called `onInteraction`, triggered during viewer interactions. The event arguments will include the type of action and the collection of variables and their values located on the parameters panel. The action type will have the string value `"Variables"`.


Here’s an example of performing actions on the client JavaScript side before applying report parameters:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->onInteraction = 'interaction';
    $viewer->process();
?>

...

<script>
    function interaction(args) {
        if (args.action == "Variables") {
            let variables = args.variables;
        }
    }
</script>
```

The collection of variables is an object containing all the variables on the parameters panel and their values, for example:


**viewer.php**

```php

var variables = {
    VariableString: "Text value",
    VariableInt: 20
}
```

It’s allowed to change the values of the variables, but the new value's type must match the type of the variable being modified. A detailed description of the available argument values can be found in the [Viewer Events](Events.md) section.


**Configuring the parameters panel**

If you don’t need to work with variables in the viewer, you can completely disable this feature. To do so, set the `showParametersButton` property to `false`.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->showParametersButton = false;
?>
```


> **Information**
>
> In this configuration, the parameters panel will not be shown even if parameters are present in the displayed report.

**Variable values during report generation**

To control all report variables, the special event `onPrepareVariables` is triggered before the report is generated. A detailed description can be found in the [Working with Report Variables](../Engine/Using_Variables.md) section.
