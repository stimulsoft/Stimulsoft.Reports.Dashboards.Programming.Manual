# Work with Parameters

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To work with report parameters in the **HTML5 Viewer**, there is a special settings panel. To add a parameter to the panel, you need to define a variable in a report requested by the user. When viewing a report in the viewer, such a variable will be automatically added to the settings panel. It supports all types of report variables (normal variables, date and time, borders, lists, etc.).


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Viewer.Work_with_Parameters_1.png)

To perform any action before applying parameters, a special **OnInteraction** event will be called when there are some interactive activities in the viewer. When you use the options panel, the type of action will have the **Variables** value.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnInteraction="StiWebViewer1_Interaction">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_Interaction(object sender, StiReportDataEventArgs e)
{
    if (e.Action == StiAction.Variables)
    {
        // The values of the variables passed from the client
        Hashtable variables = e.RequestParams.Interaction.Variables;
    }
}
...
```

When working with parameters is not required, you can disable this feature. For this, you can use the **ShowParametersButton** property. Set this property to **false** in this case.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    ShowParametersButton="false">
</cc1:StiWebViewer>
...
```


> **Information**
>
> With this viewer configuration, the parameters panel will not be displayed, even if the parameters are present in the report.
