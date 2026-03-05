# Add custom functions

You can add a custom function to the Dictionary in the report designer when you integrate it into your application. After adding the custom function, you can use this in creating reports and dashboards. Below is the example of adding a function for calculating the sum total.


**index.html**

```html
...
var myFunc = function (value) {
    if (!Stimulsoft.Data.Extensions.ListExt.isList(value))
    return Stimulsoft.Base.Helpers.StiValueHelper.tryToNumber(value);

    return Stimulsoft.Data.Functions.Funcs.skipNulls(Stimulsoft.Data.Extensions.ListExt.toList(value))
    .tryCastToNumber()
    .sum();
};

Stimulsoft.Report.Dictionary.StiFunctions.addFunction("MyCategory", "MySum", "MySum", "MySum", "", Number, "Return Description", [Object], ["value"], ["Descriptions"], myFunc);
...
```
