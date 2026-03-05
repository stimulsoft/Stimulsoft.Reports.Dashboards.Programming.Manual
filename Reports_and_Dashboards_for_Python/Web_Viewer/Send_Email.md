# Sending a report by Email

The viewer provides the ability to send a report by Email. To enable this feature, simply set the viewer's `showSendEmailButton` property to `True` and add an `onEmailReport` event handler on the Python server side, where all Email sending parameters should be specified. If necessary, a JavaScript event call can be added, in which arguments allow you to retrieve the necessary data for sending the email, get the report export type, obtain the report itself, and access the report export settings, which can be modified if needed. A detailed description of the available argument values can be found in the Viewer's Events section.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.events import StiEmailEventArgs

def emailReport(args: StiEmailEventArgs):
    settings = args.settions

viewer = StiViewer()
viewer.onEmailReport += emailReport
viewer.onEmailReport += 'emailReport'
```


**viewer.html**

```html

<script>
    function emailReport(args) {
        let settings = args.settings;
    }
</script>
```

When sending a report by Email, a menu for selecting the attachment format is displayed, which corresponds to the report export format selection menu. After choosing the format, a dialog will appear for entering the sending parameters, such as the recipient's Email, subject, and message body. After confirming the sending, the `onEmailReport` event will be triggered, where you can check and correct the data entered in this form, for example:


**viewer.html**

```html

<script>
    function emailReport(args) {
        args.settings.subject = "Invoice: " + args.settings.subject;
    }
</script>
```

Pure JavaScript doesn’t have built-in functions for working with Email, functions for this purpose are implemented on the Python server-side. To send an Email, the Python server needs to be configured with data such as the login and password of the account used for sending, as well as server settings like its address, port, and other parameters. This is done through the settings property, which is part of the event arguments and represents an object of the `StiEmailSettings` class that contains all the necessary properties. Additionally, the arguments allow you to access and modify the email's sending data (subject, body, and report file name). A detailed description of the available settings can be found in the [Viewer Events](Events.md) section.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.events import StiEmailEventArgs

def emailReport(args: StiEmailEventArgs):
    args.settings.fromAddr = 'mail.sender@stimulsoft.com'
    args.settings.host = 'smtp.stimulsoft.com'
    args.settings.port = 456
    args.settings.login = '********'
    args.settings.password = '********'
    return 'The Email has been sent successfully.'

viewer = StiViewer()
viewer.onEmailReport += emailReport
```

Example of checking and modifying the email subject before sending:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.events import StiEmailEventArgs

def emailReport(args: StiEmailEventArgs):
    if len(args.settings.subject) == 0:
        args.settings.subject = args.formatName + ' report ' + args.settings.attachmentName

viewer = StiViewer()
viewer.onEmailReport += emailReport
```

Example of adding addresses of additional recipients for the email with the report:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer
from stimulsoft_reports.events import StiEmailEventArgs

def emailReport(args: StiEmailEventArgs):
    args.settings.cc.append('extra_recipient_one@stimulsoft.com')
    args.settings.bcc.append('hidden_recipient_one@stimulsoft.com')
    args.settings.bcc.append('hidden_recipient_two@stimulsoft.com John Smith')

viewer = StiViewer()
viewer.onEmailReport += emailReport
```

### Email sending settings

The viewer allows you to set default values for the email sending form. The properties `defaultEmailAddress`, `defaultEmailSubject`, and `defaultEmailMessage` are intended for this. By default, these properties are empty.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.options.email.defaultEmailAddress = 'recipient_address@stimulsoft.com'
viewer.options.email.defaultEmailSubject = 'New Invoice'
viewer.options.email.defaultEmailMessage = 'Please check the new invoice in the attachment'
```
