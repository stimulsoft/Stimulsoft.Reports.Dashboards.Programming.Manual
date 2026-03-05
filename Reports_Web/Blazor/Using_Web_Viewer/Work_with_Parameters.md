# Work with Parameters

The support of a particular parameter panel for work with report parameters in the **Blazor Viewer** is realized. To add a parameter to the panel, you should define the variable requested from a user in a report. When viewing a report in the viewer, this variable will be added automatically to the parameter panel — all types of report variables (simple variables, date and time, borders, lists, etc.).


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Viewer.Work_with_Parameters_1.png)

Additional viewer settings are not required for working reports with parameters. If you need to take some actions before using parameters, you can define the special **OnInteraction** event.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer OnInteraction="@OnInteraction" />

@code
{
    private void OnInteraction(StiReportDataEventArgs args)
    {
        // Some code before any interaction
        // ...
    }
}
```

This event is triggered for any interactive viewer actions. If you need to make some actions only when applying report parameters, you can use value parameters in argument events. The arguments contain all necessary data and conditions of the viewer client side. To define a type of viewer actions, you should use the **Action** property.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer OnInteraction="@OnInteraction" />

@code
{
    private void OnInteraction(StiReportDataEventArgs args)
    {
        if (args.Action == StiAction.Variables)
        {
            // Some code before apply parameters
        }
    }
}
```

If the work with parameters is requested, you can disable this feature. The **ShowParametersButton** property is intended for this. This property is located in the **Toolbar** properties section, and the **false** value must be set for it.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Init options object
        Options = new StiBlazorViewerOptions();
        Options.Toolbar.ShowParametersButton = false;
    }
}
```


> **Information**
>
> Due to this viewer configuration, the parameter panel won't be shown, even if the parameters are present in a displayed report.
