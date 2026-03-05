# Sending Report by Email

The option to send a report by email is implemented in the **Blazor Viewer** component. To activate it, you should set the **ShowSendEmailButton** viewer property to true and define the **OnEmailReport** event.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Options="@Options" OnEmailReport="@OnEmailReport" />

@code
{
    //Options object
    private StiBlazorViewerOptions Options;
    
    private void OnEmailReport(StiEmailReportEventArgs args)
    {
        //args.Options.AddressTo = "";
        //args.Options.Subject = "";
        //args.Options.Body = "";
        
        // Should be filled here
        args.Options.AddressFrom = "admin_address@test.com";
        args.Options.Host = "smtp.test.com";
        args.Options.Port = 465;
        args.Options.UserName = "admin_address@test.com";
        args.Options.Password = "admin_password";
        
        //args.Options.CC.Add("email@test.com");
        //args.Options.BCC.Add("email@test.com");
        //args.Options.EnableSsl = true;
    }
}
```

The menu of attachment format selection displays when sending a report by email. This menu corresponds to the Export format menu.  After a format is selected, the parameters dialog, such as recipient`s email, theme, and text of the letter, will display.


![](../../../images/topics/Reports_Web.Blazor.Using_Web_Viewer.Send_Email_1.png)

After confirming the submission, the **OnEmailReport** event described above will be triggered, where you can check and correct data typed in this form. The exported report file will be attached to an email automatically.


The **Blazor Viewer** component allows setting values by default for the Send Email form. The **DefaultEmailAddress**, the **DefaultEmailSubject**, and **DefaultEmailMessage** properties are used for this. These properties are empty by default.


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
        Options.Email.DefaultEmailAddress = "recipient_address@gmail.com";
        Options.Email.DefaultEmailSubject = "New Invoice";
        Options.Email.DefaultEmailMessage = "Please check the new invoice in the attachment";
    }
}
```
