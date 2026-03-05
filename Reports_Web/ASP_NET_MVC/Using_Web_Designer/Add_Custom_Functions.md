# Add custom functions

> **Information**
>
> See  on [GitHub](https://github.com/stimulsoft/Samples-ASP.NET-MVC-CSharp) example of adding a custom function in the ASP.NET MVC HTML5 Designer component.

You can add a custom function to the Dictionary in the report designer when integrating it into your application. After adding the custom function, you can use this in creating reports and dashboards. Below is the example of adding a function for converting text to uppercase.


**DesignerController.cs**

```csharp
...
public static string MyFunc(string value)
{
    return value.ToUpper();
}
...
static DesignerController()
{
    var ParamNames = new string[1];
    var ParamTypes = new Type[1];
    var ParamDescriptions = new string[1];
    
    ParamNames[0] = "value";
    ParamDescriptions[0] = "Descriptions";
    ParamTypes[0] = typeof(string);
    
    // How to add my function
    StiFunctions.AddFunction(
    "MyCategory",
    "MyFunc",
    "MyFunc",
    "Description",
    typeof(DesignerController),
    typeof(string),
    "Return Description",
    ParamTypes,
    ParamNames,
    ParamDescriptions);
}
...
```
