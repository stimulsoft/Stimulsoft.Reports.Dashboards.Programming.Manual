## Options

If a report is shown in the dialog window, i.e. ability to set parameters of dialog window.


**Code**

```
...
var report: StiReport = new StiReport();
report.loadDocumentFromString(documentString);
report.showDialog(rectangle: Rectangle, title: String, allowResize: Boolean, allowDrag: Boolean);
...
```

In example 4 parameters are described:

  * **Rectangle** (position and dialog window size), is set as Rectangle (x, y, width, height), where x,y are indents from the top left corner of the application. By default Rectangle (10, 10, application.width - 20, application.height - 20);

  * **title** - is the window title. If the title is not set, then the window will have the "Viewer" title.

  * **allowResize** - this parameter allows changing window size. It may have two values: true and false. By default, the value is set to false, i.e. it is impossible to change window size.

  * **allowDrag** - this parameter allows dragging dialog window. It may have two values: true and false. The default value is false, i.e. it is impossible to drag the dialog viewer window.


A sample of setting parameters:


**Code**

```
...
var rect: Rectangle = new Rectangle(100, 100, 900, 600);
report.showDialog(rect, "Customized ViewerFx", true, true);
...
```

As seen from the sample:

  * Indent from the top left corner is 100 by x, y axes. Width 900, height 600.

  * The name of the dialog box is "Customized ViewerFx".

  * Changing size of the dialog window of viewer - possible.

  * Dragging the dialog window - possible.
