# Sending Report By Email

The viewer provides the ability to send a report by email. To enable this feature, you need to set the viewer's `showSendEmailButton` property to `true` and add an event handler for `onEmailReport`.


Pure JavaScript doesn’t have email handling functions, so this feature uses PHP server-side functions. To send an email, in the PHP server event arguments, you must set parameters such as the login and password of the account sending the email, as well as the server settings — its address, port, and other details. This is done through the `$args->settings` property in the event arguments. This property is an object of the `StiEmailSettings` class, containing all the necessary email sending parameters.


Here is an example of sending a report by email with the minimum required parameters:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    use Stimulsoft\Events\StiEmailEventArgs;
    use Stimulsoft\Report\StiReport;
    use Stimulsoft\StiResult;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->showSendEmailButton = true;
    
    $viewer->onEmailReport = function (StiEmailEventArgs $args) {
        $args->settings->from = 'mail.sender@stimulsoft.com';
        $args->settings->host = 'smtp.stimulsoft.com';
        $args->settings->login = '********';
        $args->settings->password = '********';
        
        return StiResult::getSuccess('The Email has been sent successfully.');
    };
    
    $viewer->process();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Sending%20a%20Report%20by%20Email.php).


Additionally, the event arguments allow you to retrieve and modify the email details (such as the subject, message, and report file name), get the report itself, and access or modify the report export settings if needed. A detailed description of available event arguments is in the [Viewer Events](Events.md) section.


If necessary, a JavaScript event can also be triggered, where you can access data required for sending the email, the export type of the report, and the report itself, as well as export settings to modify them if needed.


Here’s an example of modifying the email subject before sending:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->showSendEmailButton = true;
    $viewer->onEmailReport = 'emailReport';
    $viewer->process();
?>

...

<script>
    function emailReport(args) {
        args.settings.subject = "Invoice: " + args.settings.subject;
    }
</script>
```

When sending an email, the JavaScript event (if defined) will be triggered first, followed by the PHP server event. This allows you to validate and adjust values right before sending the email.


Example of checking and modifying the email subject on the PHP server-side before sending:


**viewer.php**

```php

$viewer->onEmailReport = function (StiEmailEventArgs $args) {
    if (strlen($args->settings->subject ?? '') == 0)
        $args->settings->subject = "{$args->formatName} report {$args->settings->attachmentName}";
    
    return StiResult::getSuccess('The Email has been sent successfully.');
};
```

Example of adding additional recipients to the email with the report:


**viewer.php**

```php

$viewer->onEmailReport = function (StiEmailEventArgs $args) {
    $args->settings->cc[] = 'extra_recipient_one@stimulsoft.com';
    $args->settings->bcc[] = 'hidden_recipient_one@stimulsoft.com';
    $args->settings->bcc[] = 'hidden_recipient_two@stimulsoft.com John Smith';
    
    return StiResult::getSuccess('The Email has been sent successfully.');
};
```

**Email sending settings**

The viewer allows you to set default values for the email dialog. These are controlled by the properties `defaultEmailAddress`, `defaultEmailSubject`, and `defaultEmailMessage`. By default, these properties are empty.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->showSendEmailButton = true;
    $viewer->options->email->defaultEmailAddress = 'recipient_address@stimulsoft.com';
    $viewer->options->email->defaultEmailSubject = 'New Invoice';
    $viewer->options->email->defaultEmailMessage = 'Please check the new invoice in the attachment';
?>
```
