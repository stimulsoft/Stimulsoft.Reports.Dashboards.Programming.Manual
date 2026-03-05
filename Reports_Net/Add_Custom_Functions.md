# Add custom functions

> **Information**
>
> When working in the report designer and using undo/redo commands, the operation stack is saved as JSON. However, if it is necessary to save the operation stack as XML, you should set the option `StiOptions.Designer.UndoRedoMode = StiUndoRedoMode.Xml`.

You can add a custom function to the Dictionary in the report designer when you integrate it into your application. After adding the custom function, you can use this in creating reports and dashboards. Below is the example of adding a function for calculating the sum total.


**Designer.cs**

```csharp
...
StiFunctions.AddFunction("MyCategory", "MySum", 
"description", typeof(MyClass), 
typeof(decimal), "Calculates a sum of the specified set of values.", 
new[] { typeof(object) }, 
new[] { "values" }, 
new[] { "A set of values" }).UseFullPath = false;
...
public static decimal MySum(object value)
{
    if (!ListExt.IsList(value))
    return Stimulsoft.Base.Helpers.StiValueHelper.TryToDecimal(value);
    return Stimulsoft.Data.Functions.Funcs.SkipNulls(ListExt.ToList(value)).TryCastToDecimal().Sum();
}
...
```
