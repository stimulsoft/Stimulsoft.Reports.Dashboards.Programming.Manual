# Saving a Report

The designer provides two options for saving a report, available in the main menu and on the main toolbar: **Save** and **Save As**. Each of these saving options has its own modes and settings.

### Saving a report on the client-side of JavaScript

When the **Save** button is clicked, the report template file is saved using the browser's functionality, and no additional settings are required. If you need to save the report using custom methods, the `onSaveReport` event is provided. The event arguments will include the report file name and the report itself. For example, the report can be saved as a JSON string and sent to the server using custom methods.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner

designer = StiDesigner()
designer.onSaveReport += 'saveReport'
```


**designer.html**

```html

<script>
    function saveReport(args) {
        let fileName = args.fileName;
        let report = args.report;
        
        let jsonReport = report.saveToJsonString();
    }
</script>
```

If the event is defined, after its completion, the designer continues to work without any additional actions or messages. If necessary, after saving the report, a dialog box with an error or text message can be displayed. For this purpose, there is a special function `StiError.showError()`. You determine whether displaying an error message is necessary.


**designer.html**

```html

<script>
    function saveReport(args) {
        let fileName = args.fileName;
        let report = args.report;
        
        // Error message
        Stimulsoft.System.StiError.showError("An error occurred while saving the report.");
        
        // Info message
        Stimulsoft.System.StiError.showError("The report was saved successfully.", true, true);
    }
</script>
```

When the **Save As** button is clicked, a dialog box will appear requesting the report file name. After that, the report template file will be saved using the browser's built-in functionality. If you need to save the report using your own methods, the `onSaveAsReport` event is provided. The event arguments will include the report file name and the report itself.


The behavior of this event is the same as the `onSaveReport` event, except that after the event is completed, the report template will be automatically saved on the computer using the browser's functionality. To prevent this action, you can set the `preventDefault` property to `true` in the event arguments, which will stop the automatic saving.


**app.py**

```python

from stimulsoft_reports.designer import StiDesigner

designer = StiDesigner()
designer.onSaveAsReport += 'saveAsReport'
```


**designer.html**

```html

<script>
    function saveAsReport(args) {
        args.preventDefault = true;
    }
</script>
```

If necessary, you can access the original report name or the name from the save dialog as follows:


**designer.html**

```html

<script>
    function saveAsReport(args) {
        // Report name from the designer save dialog
        var reportName1 = args.fileName;
        
        // Original report name from properties
        var reportName2 = args.report.reportName;
    }
</script>
```

A detailed description of available argument values can be found in the [Designer Events](Events.md) section.

### Saving the report on the Python server-side

To save the report on the Python server-side, simply define the `onSaveReport` event. The event arguments will include the report file name and the report itself as an object. You can use standard functions to save the report, for example, saving the edited report as a file in a specified directory:


**app.py**

```python

import json
import os
from stimulsoft_reports import StiResult
from stimulsoft_reports.designer import StiDesigner
from stimulsoft_reports.events import StiReportEventArgs
from stimulsoft_reports.report import StiReport

def saveReport(args: StiReportEventArgs):
    filePath = os.path.normpath(os.getcwd() + '\\static\\reports\\' + args.fileName)
    try:
        with open(filePath, mode='w', encoding='utf-8') as file:
            jsonReport = json.dumps(args.report, indent = 4)
            file.write(jsonReport)
            file.close()
    except Exception as e:
        return StiResult.getError(str(e))

    return f'The report was successfully saved to a {args.fileName} file.'

designer = StiDesigner()
designer.onSaveReport += saveReport
```

Similarly, the `onSaveAsReport` event works on the Python server-side, with all event arguments having the same names and values.


A detailed description of the available argument values can be found in the [Designer Events](Events.md) section.
