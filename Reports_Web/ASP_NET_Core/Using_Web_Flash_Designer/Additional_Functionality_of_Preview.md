# Additional Features of Preview

The preview window of the **Flash Designer** component is a fully functional interactive **Flash Viewer** that can print and export reports, supports working with report parameters, interactive reports and sending them via email. To use these features, you do not need any additional settings for the report designer. The actions below are required for proper working with the embedded report viewer.


**Index.cshtml**

```
...
@Html.StiNetCoreDesignerFx(new StiNetCoreDesignerFxOptions() {
Actions =
    {
        ExportReport = "ExportReport",
        EmailReport = "EmailReport"
    },
    PreviewToolbar =
    {
        ShowSendEmailButton = true
    }
})
...
```


**HomeController.cs**

```csharp
...
public IActionResult ExportReport()
{
    StiReport report = StiNetCoreDesignerFx.GetReportObject(this);
    // ...
    
    return StiNetCoreDesignerFx.ExportReportResult(this, report);
}

public IActionResult EmailReport()
{
    StiEmailOptions options = StiNetCoreViewerFx.GetEmailOptions(this);
    
    // Passed from the viewer, can be checked and changed
    // options.AddressTo = "";
    // options.Subject = "";
    // options.Body = "";
    
    // Should be filled here
    options.AddressFrom = "admin_address@test.com";
    options.Host = "smtp.test.com";
    options.Port = 465;
    options.UserName = "admin_address@test.com";
    options.Password = "admin_password";
    
    // options.CC.Add("email@test.com");
    // options.BCC.Add("email@test.com");
    // options.EnableSsl = true;
    
    return StiNetCoreDesignerFx.EmailReportResult(this, options);
}
...
```


![](../../../images/topics/Reports_Web.ASP_NET_Core.Using_Web_Flash_Designer.Additional_Functionality_of_Preview_1.png)

In any of the above actions, you can manipulate the report template, for example, change its properties and parameters, connect new data for rendering.


> **Information**
>
> If exporting a report or sending an email with the report is not required, it is allowed not to set the specified actions. In this case, the corresponding menus in the embedded report viewer will be hidden.
