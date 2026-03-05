# Add custom functions

> **Information**
>
> See  on [GitHub](https://github.com/stimulsoft/Samples-ASP.NET-CSharp) example of adding a custom function in the ASP.NET HTML5 Designer component.

You can add a custom function to the **Dictionary** in the report designer when integrating it into your application. After adding the custom function, you can use this in creating reports and dashboards. Below is the example of adding a function for calculating the sum total.


**Default.aspx.cs**

```csharp
...
public static decimal MySum(object value)
{
    if (!ListExt.IsList(value))
    return Stimulsoft.Base.Helpers.StiValueHelper.TryToDecimal(value);

    return Stimulsoft.Data.Functions.Funcs.SkipNulls(ListExt.ToList(value))
    .TryCastToDecimal()
    .Sum();
}
...
static _Default()
{
    StiFunctions.AddFunction("MyCategory", "MySum",
    "description", typeof(_Default),
    typeof(decimal), "Calculates a sum of the specified set of values.",
    new[] { typeof(object) },
    new[] { "values" },
    new[] { "A set of values" }).UseFullPath = false;
}
...
```
