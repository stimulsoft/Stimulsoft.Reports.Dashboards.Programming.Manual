# Sending Report by Email

The **Angular Viewer** component provides the ability to send reports by email. To activate this feature, you should set the **ShowSendEmailButton** property of the viewer to **true**, and define the **EmailReport** action.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Actions.EmailReport = "EmailReport";
    options.Toolbar.ShowSendEmailButton = true;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}

public IActionResult EmailReport()
{
    StiEmailOptions options = StiAngularViewer.GetEmailOptions(this);
    
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
    
    return StiAngularViewer.EmailReportResult(this, options);
}
...
```

When sending a report by email, the menu to select the attachment format is displayed. It corresponds to the menu for selecting the format for exporting the report. After selecting the format, the dialog to enter send email parameters, such as the recipient's email, subject and text of the message is displayed.


![](../../../images/topics/Reports_Web.Angular.Using_Web_Viewer.Send_Email_1.png)

After confirmation of sending the email the above described **EmailReport** event will be called. You can check and correct the data entered in this form. The exported report file will be attached to the email automatically.


The **Angular Viewer** component allows you to set default values for the send email form. The **DefaultEmailAddress**, **DefaultEmailSubject** and **DefaultEmailMessage** properties can be used for this. By default, these properties are empty.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Email.DefaultEmailAddress = "recipient_address@gmail.com";
    options.Email.DefaultEmailSubject = "New Invoice";
    options.Email.DefaultEmailMessage = "Please check the new invoice in the attachment";
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```
