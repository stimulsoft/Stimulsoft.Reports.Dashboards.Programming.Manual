# Additional Features of Designer

In addition to the basic editing and previewing capabilities, **Flash Designer** has several additional features.


If necessary, it is possible to view the C#/VB.Net code of an editable report template on a separate designer tab. By default, it is disabled. To enable it, you should set the **ShowCodeTab** property to **true**. A special **DesignerEvent** action should also be defined.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesignerFx("MvcDesignerFx1", 
    new StiMvcDesignerFxOptions() {
        Actions =
        {
            DesignerEvent = "DesignerEvent"
        },
        Toolbar =
        {
            ShowCodeTab = true
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult DesignerEvent()
{
    return StiMvcDesignerFx.DesignerEventResult();
}
...
```


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Flash_Designer.Additional_Features_of_Designer_1.png)


> **Information**
>
> If any errors occurred during the report compilation, they will be displayed in a separate dialog box as a list. Double-clicking on the selected compilation error will display the specified C#/VB.Net code window, and the insertion cursor will be moved to the position at which this error occurred.

The main menu of the **Flash Designer** component contains the **Exit** item, selecting which a special **Exit** action is called. If it is absent, then transition to the address specified in the URL settings.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesignerFx("MvcDesignerFx1", 
    new StiMvcDesignerFxOptions() {
        Actions =
        {
            Exit = "DesignerExit"
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult DesignerExit()
{
    return View("MainPage");
}
...
```

In the **Exit** action method, you can jump to the required view. You can also specify the URL address using the **ExitUrl** property.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesignerFx("MvcDesignerFx1", 
    new StiMvcDesignerFxOptions() {
        Behavior =
        {
            ExitUrl = "http://www.stimulsoft.com"
        }
})
...
```

If the **Exit** action and the **ExitUrl** property are not specified, then the corresponding item in the main menu of the designer will be hidden.
