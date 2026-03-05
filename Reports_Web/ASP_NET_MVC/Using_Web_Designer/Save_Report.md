# Saving Reports and Dashboards

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **HTML5 Designer** component provides two ways of saving the report which are available in the main menu and in the main panel of the designer - **Save Report** and **Save As**. In turn, each of these ways has its own modes and settings.


### Saving a report and dashboard on the server side

To save the editable report on the server-side, you need to set the **SaveReport** action, which will be called when you select Save in the main menu or click the Save button on the main panel of the designer.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesigner("MvcDesigner1", 
    new StiMvcDesignerOptions() {
        Actions =
        {
            SaveReport = "SaveReport"
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult SaveReport()
{
    StiReport report = StiMvcDesigner.GetReportObject();
        
    // Save the report template
    // ...
    
    return StiMvcDesigner.SaveReportResult();
}
...
```

This action returns a response to the client-side of the designer about the result of saving the report. After saving the report, it is possible to display a dialog box with an error or a text message.


**HomeController.cs**

```csharp
...
public ActionResult SaveReport()
{
    StiReport report = StiMvcDesigner.GetReportObject();
        
    // Save the report template
    // ...
    
    // Completion of the report saving with message dialog box
    return StiMvcDesigner.SaveReportResult("Some message after saving");
}
...
```

You can get a report name from the designer save dialog or an original report name.


**HomeController.cs**

```csharp
...
public ActionResult SaveReport()
{
    var requestParams = StiMvcDesigner.GetRequestParams();
    var report = StiMvcDesigner.GetReportObject();
    
    //Report name from designer save dialog
    var savingReportName = requestParams.Designer.FileName; 
    
    //Original report name from properties
    var originalReportName = report.ReportName; 
    
    return StiMvcDesigner.SaveReportResult();
}
...
```

In this case, the dialog with the specified text will be displayed. The text can contain both an error message of saving or a warning or any other message.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Designer.Save_Report_1.png)


### Saving reports and dashboards on the client side

To save the edited report on the client-side as a file, no additional designer settings are required. It is enough to click the **Save As** main menu item. The dialog box will be displayed. In this dialog, you can change the name of the report file. The file will be saved to the local disk of the computer.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Designer.Save_Report_2.png)

The **HTML5 Designer** component provides the ability to change the behavior of the specified save option. For this purpose, the special **SaveReportAs** action is used in the designer. If you use this event, the report will be saved on the server-side. The work of this event will be similar to the **SaveReport** action.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesigner("MvcDesigner1", 
    new StiMvcDesignerOptions() {
        Actions =
        {
            SaveReportAs = "SaveReportAs"
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult SaveReportAs()
{
    StiReport report = StiMvcDesigner.GetReportObject();
        
    // Save the report template
    // ...
    
    return StiMvcDesigner.SaveReportResult();
}
...
```


### Saving settings

The report is saved in the background mode without reloading the page in the web browser window. Suppose you need to control the process of saving the report visually. In that case, you should change the value of the **SaveReportMode** (or **SaveReportAsMode**) property of the designer to one of the three specified values - **Hidden** (default value), **Visible**, or **NewWindow**.

**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcDesigner("MvcDesigner1", 
    new StiMvcDesignerOptions() {
        Actions =
        {
            SaveReportAs = "SaveReportAs"
        },
        Behavior =
        {
            SaveReportAsMode = StiSaveMode.Visible
        }
})
...
```

If the **SaveReportMode** property is set to **Visible**, the report save action will be called in the current browser window in the normal (visible) mode using the POST request. If the **SaveReportMode** property is set to **NewWindow**, the report save event will be called in a new window of the web browser. By default, this property is set to **Hidden** - the report save event is called in the background using the AJAX request and is not displayed in the browser window. The same values and behavior are applicable to the **SaveReportAsMode** property.
