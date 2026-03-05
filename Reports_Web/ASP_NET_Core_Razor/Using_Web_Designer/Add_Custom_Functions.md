# Add custom functions

> **Information**
>
> See  on [GitHub](https://github.com/stimulsoft/Samples-NET-6.0-Razor-CSharp) example of adding a custom function in the ASP.NET MVC HTML5 Designer component.

You can add a custom function to the Dictionary in the report designer when you integrate it into your application. After adding the custom function, you can use this in creating reports and dashboards. Below is the example of adding a function for calculating the sum total.


**Index.cshtml.cs**

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
static IndexModel()
{
    StiFunctions.AddFunction("MyCategory", "MySum",
    "description", typeof(DesignerController),
    typeof(decimal), "Calculates a sum of the specified set of values.",
    new[] { typeof(object) },
    new[] { "values" },
    new[] { "A set of values" }).UseFullPath = false;
}
...
```
