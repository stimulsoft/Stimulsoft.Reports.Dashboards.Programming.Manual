# Get Started JS

This example shows how to install and run Stimulsoft JS for Browser. Also, you can find more samples [Reports.JS](https://github.com/stimulsoft/Samples-JS) and [Dashboards.JS](https://github.com/stimulsoft/Samples-Dashboards-JS) on the GitHub.


**Step 1**: Open your html file in editor. For example, **index.html**.


**Step 2**: Add reference to viewer **CSS file** in HTML head:


**index.html**

```html
...
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>JS Project</title>
    
    <link href="https://unpkg.com/stimulsoft-dashboards-js/Css/stimulsoft.viewer.Office2022.whiteblue.css" rel="stylesheet"/>
    
    //Also, you must to specify designer css file link, if you need to use js designer
    <link href="https://unpkg.com/stimulsoft-dashboards-js/Css/stimulsoft.designer.Office2022.whiteblue.css" rel="stylesheet"/>
</head>
</html>
...
```

**Step 3**: Add the references to stimulsoft js scripts in HTML head.


**index.html**

```html
...
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>JS Project</title>
        
    <link href="https://unpkg.com/stimulsoft-dashboards-js/Css/stimulsoft.viewer.Office2022.whiteblue.css" rel="stylesheet"/>
    
    //Also, you must to specify designer css file link, if you need to use js designer
    <link href="https://unpkg.com/stimulsoft-dashboards-js/Css/stimulsoft.designer.Office2022.whiteblue.css" rel="stylesheet"/>
    
    <script src="https://unpkg.com/stimulsoft-reports-js/Scripts/stimulsoft.reports.js" type="text/javascript"></script>
    
    //Also, you must to specify dashboard script link, if you need to use dashboards
    <script src="https://unpkg.com/stimulsoft-dashboards-js/Scripts/stimulsoft.dashboards.js" type="text/javascript"></script>
    <script src="https://unpkg.com/stimulsoft-reports-js/Scripts/stimulsoft.viewer.js" type="text/javascript"></script>
    
    //Also, you must to specify designer script link, if you need to use js designer
    <script src="https://unpkg.com/stimulsoft-reports-js/Scripts/stimulsoft.designer.js" type="text/javascript"></script>
</head>
</html>
...
```


> **Information**
>
> It is important to follow the order in which scripts are connected:
>
> - The **stimulsoft.reports.js** script should be the first;
>
> - The **stimulsoft.viewer.js** script must be earlier than **stimulsoft.designer.js** script.

**Step 4**: Create the **onLoad()** function and a new viewer, if you want to show report or dashboard.


**index.html**

```html
...
<script type="text/javascript">
function onLoad(){
    // Create the report viewer with default options
    var viewer = new Stimulsoft.Viewer.StiViewer(null, "StiViewer", false);
    
    // Show the report viewer in div content
    viewer.renderHtml("content");
}
</script>
...
//Call function onLoad() and put viewer in <div>.
<body onLoad="onLoad()">
    <div id="content">Component should be here</div>
</body>
...
```

**Step 5**: Create a new report object, load a report template file in it, and assign report object to the report viewer.


**index.html**

```html
...
<script type="text/javascript">
function onLoad(){
...
    // Create a new report object
    var report = new Stimulsoft.Report.StiReport();
    
    // Load report template in the report object
    report.loadFile("report url");
    
    // Assign report object to report viewer
    viewer.report = report;
...
}
</script>
...
```

**Step 6**: Create the **onLoad()** function and a new designer, if you want to create or edit report or dashboard.


**index.html**

```html
...
<script type="text/javascript">
function onLoad(){
    // Create the report designer with default options
    var designer = new Stimulsoft.Designer.StiDesigner(null, "Designer", false);
    
    // Show the report designer in div content
    designer.renderHtml("content");
    
    // Create a new report object
    var report = new Stimulsoft.Report.StiReport();
    
    // Load report template in the report object
    report.loadFile("report url");
    
    // Assign report object to report designer
    designer.report = report;
}
</script>
...
//Call function onLoad() and put designer in <div>.
<body onLoad="onLoad()">
    <div id="content">Component should be here</div>
</body>
...
```

**Step 7**: Save changes and open **index.html** file in browser.
