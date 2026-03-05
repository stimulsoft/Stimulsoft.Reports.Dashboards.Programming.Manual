# Showing Reports

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.


> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `report.render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer.

To show the report, you should add the scripts and styles required for the **StiViewer** component to the HTML page of a project.

**viewer.html**

```html
...
<script src="scripts/stimulsoft.reports.js" type="text/javascript"></script>
<script src="scripts/stimulsoft.dashboards.js"></script>
<script src="scripts/stimulsoft.viewer.js" type="text/javascript"></script>
...
```

Then you should add JavaScript code of report loading to the HTML page, and assign the resulting object to the viewer. In this case, the viewer will be deployed in the current DOM element at the place where the script is located.


**viewer.html**

```html
...
<script type="text/javascript">
    var report = new Stimulsoft.Report.StiReport();
    report.loadFile("SimpleList.mrt");
    //report.loadFile("Dashboard.mrt");
    
    var viewer = new Stimulsoft.Viewer.StiViewer();            
    viewer.report = report;
</script>
...
```


![](../../images/topics/Reports_JS.Web_Viewer.Showing_Reports_1.png)

You can create a **StiViewer** object using the **Stimulsoft.Viewer.StiViewer()** constructor, which can accept non-required arguments as input:
* **options** is a set of options that can be found in the **Stimulsoft.Viewer.StiViewerOptions** class. All options are split into categories. A detailed description of the categories and options can be found in the [Viewer Settings](Settings.md) topic.

* **viewerId** - viewer identification is used when **deploying a component as a DOM object, the default value is “StiViewer”.**
* **renderAfterCreate** - defines the viewer location. If it is set to **true**, the viewer will be displayed in the same place in the DOM tree where code to create an object is placed. If it is set to **false**, the viewer will be located at the place where the **renderHtml()** method is called. For example, this can be the initialization of the viewer in the page header.


**viewer.html**

```html
...
<script type="text/javascript">
    var viewer = new Stimulsoft.Viewer.StiViewer(null, "StiViewer", false);
</script>
...
```

And the subsequent output of the viewer in the current DIV element.

**viewer.html**

```html
...
<div>Page content</div>
<div>
    <script type="text/javascript">
    // Render the report viewer in this place
        viewer.renderHtml();
    </script>
</div>
...
```

As an argument of the **renderHtml(id)** output method of the viewer, it is allowed to specify the element identifier of the HTML page in which the viewer should be displayed.

**viewer.html**

```html
...
<script type="text/javascript" >
    var viewer = new Stimulsoft.Viewer.StiViewer(null, "StiViewer", false);
    viewer.renderHtml("content");
</script>
...
```

The specified element must be located on the HTML page on which the report viewer is used.


**viewer.html**

```html
...
<div id="content"></div>
...
```
