# Saving Reports

There are two options of saving reports in the **Blazor Designer** component, which are available in the main menu and the main panel of the designer - **Save** and **Save as**. At the same time, each of these options of saving has its modes and settings.


### Saving reports on the server-side

To save an edited report on the server-side, you should define the **OnSaveReport** event, which will be invoked when selecting the **Save** item in the main menu or clicking the **Save** in the main panel of the designer.


**Index.razor**

```
@using Stimulsoft.Base
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorDesigner Report="@Report" OnSaveReport="@OnSaveReport"/>

@code
{
    //Report object to use in designer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Create empty report object
        var report = new StiReport();
        
        //Load report template
        report.Load("Reports/TwoSimpleLists.mrt");
        
        //Assing report object to designer
        Report = report;
    }
    
    private void OnSaveReport(StiSaveReportEventArgs args)
    {
        args.Report.Save("Reports/TwoSimpleLists.mrt");
    }
}
```

The **OnSaveReport** event will be invoked when clicking **Save**. The edited report will be passed in the event arguments. If required, you can use the option of displaying the dialog window with an error or a text message after saving a report. The **ErrorCode** and **ErrorString** properties in the arguments of the event are used for this.


**Index.razor**

```
...
private void OnSaveReport(StiSaveReportEventArgs args)
{
    args.Report.Save("Reports/TwoSimpleLists.mrt");
    
    args.ErrorString = "Some message after saving";
}
...
```

In this case, the dialog window with a specified text will be displayed. The text can contain either a save error or a warning message or any other message.


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Designer.Save_Report_1.png)

If required, you can access the original report name or report name from the save dialog.


**Index.razor**

```
...
private void OnSaveReport(StiSaveReportEventArgs args)
{
    //Report name from designer save dialog
    var savingReportName = args.FileName;
    
    //Original report name from properties
    var originalReportName = args.Report.ReportName; 
}
...
```


### Saving on the client-side

To save an edited report on the client-side as a file, you don't need additional designer settings. It's enough to select **Save as**, when clicking on it, the file saving dialog will be displayed. In this dialog, you can change the name of your report file, and after that, the file will be saved on the local disk of the computer.


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Designer.Save_Report_2.png)

The **Blazor Designer** component changes the behavior of the specified saving variant; there is the **OnSaveReportAs** event for this. When specifying this action, a report will be saved on the server-side; the work of this action will be analogous to the **OnSaveReportAs** event.


**Index.razor**

```
...
private void OnSaveReportAs(StiSaveReportAsEventArgs args)
{
    args.Report.Save("Reports/TwoSimpleLists.mrt");
}
...
```


### Saving settings

A report is saved in the background mode, i.e., without reloading a page in the browser window. Suppose it is required to control the process of report saving somehow visually. In that case, you should change the **SaveReportMode** option (or the **SaveReportAsMode** option) to one of three values - **Hidden** (set by default), the **Visible**, or the **NewWindow**.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorDesigner Report="@Report" Options="@Options" />

@code
{
    //Report object to use in designer
    private StiReport Report;
    
    private StiBlazorDesignerOptions Options;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Init options object
        Options = new StiBlazorDesignerOptions();
        Options.Behavior.SaveReportMode = StiSaveMode.Visible; 
        Options.Behavior.SaveReportAsMode = StiSaveMode.Visible;
    }
}
```

If the **SaveReportMode** option is set to **Visible**, report saving will be invoked in the current window of the browser in a simple (visible) mode with the help of the POST request. If the **SaveReportMode** option is set to the **NewWindow** value, the save report event will be invoked in a new browser window. This option is set to the **Hidden** value by default, i.e., the report saving is invoked in the background with the help of the AJAX request, and it is not displayed in the browser window. The same values and behavior are available for the **SaveReportAsMode** option.
