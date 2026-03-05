# License Activation

After purchasing the product, you need to activate the license for the components you intend to use. There are several ways to apply the license key.


### Activation using code string

To activate the product using a license string, simply copy the encrypted license text from your [personal account on the website](https://auth.stimulsoft.com/#/login) and register it using the static setKey() function from the StiLicense class:


**app.py**

```python

from stimulsoft_reports import StiLicense

StiLicense.setKey('Your activation code...')
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


### Activation using file

To activate the product using a license file, download the license.key file from your [personal account on the website](https://auth.stimulsoft.com/#/login) and place it into your web project folder (for example, into the static folder). Then, register the license using the static setKey() function from the StiLicense class:


**app.py**

```python

from stimulsoft_reports import StiLicense

StiLicense.setFile(url_for('static', filename='license.key'))
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.Python).


### Activation of the report generator only

In some cases, you may need to activate only the report generator, separately from the other components. In this case, you can register the license key using the setKey() or setFile() methods of the license property on the report object:


**app.py**

from stimulsoft_reports.report import StiReport
report = StiReport()report.license.setKey('Your activation code...')
# report.license.setFile(url_for('static', filename='license.key'))


> **Information**
>
> The report viewer and report designer components also have a license property that can be used in the same way to manage the license key.

**Protection against license key theft**

When using a license string, you can add it conditionally in your code. For example, if the sessionID variable holds the client’s current session information, you may want to add the license key only for authorized users:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()

if sessionID != None:
    report.license.setKey('Your activation code...')
```

It is also a good idea to change the location and filename of the license key file. For example:


**app.py**

```python

from stimulsoft_reports.report import StiReport

report = StiReport()
report.license.setFile(url_for('private', filename='a15fc0ef64e6.key'))
```
