# Editing Reports

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **StiDesigner** component is a tool for creating and editing reports. To start working with the report designer, you should add the scripts and styles required for the component to the HTML page of the project.


**designer.html**

```html
...
<script src="scripts/stimulsoft.reports.js" type="text/javascript"></script>
<script src="scripts/stimulsoft.dashboards.js"></script>
<script scr="scripts/stimulsoft.viewer.js" type="text/javascript"></script>
<script src="scripts/stimulsoft.designer.js" type="text/javascript"></script>
...
```

To edit report event scripts using the Blockly tool in the designer, additionally you should add an appropriate script file, which contains a visual part of editor:


**designer.html**

```html
...
<script src="scripts/stimulsoft.reports.js" type="text/javascript"></script>
<script src="scripts/stimulsoft.dashboards.js"></script>
<script scr="scripts/stimulsoft.viewer.js" type="text/javascript"></script>
<script src="scripts/stimulsoft.designer.js" type="text/javascript"></script>
<script src="scripts/stimulsoft.blockly.editor.js" type="text/javascript"></script>
...
```


> **Information**
>
> Also, you need to add the scripts and styles for the report viewer, because this component is used to preview reports on the corresponding designer tab.

Then you should add the JavaScript code of report loading to the HTML page and assign the resulting object to the designer.


**designer.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("SimpleList.mrt");
//report.loadFile("Dashboard.mrt");

var designer = new Stimulsoft.Designer.StiDesigner(null, "Designer", false);
designer.report = report;
...
```


![](../../images/topics/Reports_JS.Web_Designer.Add_Designer_1.png)

You can create a **StiDesigner** object using the **Stimulsoft.Designer.StiDesigner()** constructor, which can take the following optional arguments as input:

* **options** – is a set of options that can be found in the **Stimulsoft.Designer.StiDesignerOptions** class. All options are divided into categories. A detailed description of the categories and options can be found in the chapter [Designer Settings](Settings.md).

* **designerId** – designer ID, used when deploying a component as a DOM object, the default value is **StiDesigner**.

* **renderAfterCreate** – defines the designer location. If it is set to **true**, the designer will be displayed in the same place in the DOM tree where the code to create an object is located. If it is set to **false**, the designer will be located at the place where the **renderHtml()** method is called. For example, this can be the initialization of the designer in the page header.


**designer.html**

```html
...
<script type="text/javascript">
    var designer = new Stimulsoft.Designer.StiDesigner(null, "StiDesigner", false);
</script>
...
```


And the subsequent output of the designer in the current DIV element.


**designer.html**

```html
...
<div>Page content</div>
<div>
    <script type="text/javascript">
        // Render the report designer in this place
        designer.renderHtml();
    </script>
</div>
...
```


As an argument of the **renderHtml(id)** designer output method, it is allowed to specify the element identifier of the HTML page in which the designer should be displayed.


**designer.html**

```html
...
<script type="text/javascript" >
    var designer = new Stimulsoft.Designer.StiDesigner(null, "StiDesigner", false);
    designer.renderHtml("content");
</script>
...
```


The specified element must be located on the HTML page on which the report designer is used.


**designer.html**

```html
...
<div id="content"></div>
...
```

Two methods of the **StiReport** object are used to load a report – **loadFile()** and **load()**. They are used as follows:

* loadFile(filePath) – loads a report from the **MRT** file which path is specified in the filePath;

* load(str) – loads a report from the string str, that contains **XML** or **JSON**;

* load(data) – loads a report from the **array data** of the number[] type;

* load(xml) – loads a report from the XML of the **XMLDocument** type;

* load(json) – loads a report from the **JS** object.


For example, use the code below to load a report from file:


**designer.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("SimpleList.mrt");
...
```

The **MRT** format of Stimulsoft Reports is the **JSON** based description of reports. You can use **MRT** files, created in other Stimulsoft Reports designers in the **JSON** based description. Use the code below to save a report to a string:


**designer.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
var jsonString = report.saveToJsonString();
...
```

Use the code below to load a report from this string:


**designer.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.load(jsonString);
...
```
