# Calling Designer from Viewer

The **HTML5 Viewer** component has the ability to call the report designer. The special **Design** button in the toolbar of the viewer (the button is disabled by default) should be used. To use this feature, you should set the **showDesignButton** property to **true**, and also to define the **onDesignReport** event handler.


**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.toolbar.showDesignButton = true;
...
```


**viewer.html**

```html
...
viewer.onDesignReport = function (args) {
    window.open("https://www.stimulsoft.com?reportName=" + args.report.reportName);
}
...
```


> **Information**
>
> The viewer does not run the designer itself, it only calls the specified event and passes the previewed report as arguments. In the event, you can set redirect to the HTML page, on which the report designer is placed.
