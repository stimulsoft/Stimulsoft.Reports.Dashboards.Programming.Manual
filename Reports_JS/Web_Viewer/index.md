# HTML5 Viewer

> **YouTube** [for the JS HTML5 Viewer](https://www.youtube.com/watch?v=jdKrggDTIws&list=PL-72PPAq-3SVanYQ9GVxG6TBITDcveRXx&index=16)


> **Samples**
>
> See [GitHub](https://github.com/stimulsoft/Samples-JS) examples for working with the JS HTML5 Viewer component. All examples are separate projects, grouped into one solution for Visual Studio.

The **HTML5 Viewer** (**StiViewer**) component is designed to view reports in the web browser. You do not need to install the .NET Framework, ActiveX components or any special plug-ins on the client side. All that is needed is any modern Web browser.


With help of **HTML5 Viewer**, you can view, print and export reports on any computer with any operating system installed. Since the viewer only uses HTML and JavaScript technologies, it can be run on devices where there is no Flash or Silverlight support - tablets, smartphones. Also, the viewer supports Mobile and Touch interfaces, which automatically enable when using mobile devices and touch screen monitors.


The **HTML5 Viewer** component uses the **JavaScript** technology to perform all actions (uploading a report, paging, scaling, interactivity in reports, etc.), which allows you to get rid of reloading the entire page and speed up work.


**HTML5 Viewer** supports many themes, animated interface, bookmarks, interactive reports, editing of report elements on the page, full screen mode, search panel, and other necessary functionality for viewing reports.


> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To use the **HTML5 Viewer** in project, you need to install the npm package of [stimulsoft-reports-js](https://www.npmjs.com/package/stimulsoft-reports-js):
npm install stimulsoft-reports-js

If this is not possible, you should add the following scripts to the project.


**viewer.html**

```html
...
<script src="scripts/stimulsoft.report.js"></script>
<script scr="scripts/stimulsoft.viewer.js"></script>
...
```

Install the npm package to use the HTML5 Viewer in a project to view reports and dashboards [stimulsoft-dashboards-js](https://www.npmjs.com/package/stimulsoft-dashboards-js):
npm install stimulsoft-dashboards-js

If this is not possible, you should add the following scripts to the project.


**viewer.html**

```html
...
<script src="Scripts/stimulsoft.reports.js"></script>
<script src="Scripts/stimulsoft.dashboards.js"></script>
<script src="Scripts/stimulsoft.viewer.js"></script>
...
```


> **Information**
>
> The script variants that you can use in your projects can be found in the [Scripts of Reports.JS Package](../../Deployment/Files_in_Reports_JS_Package.md) and [Scripts of Dashboards.JS Package](../../Deployment/Scripts_in_Dashboards_JS_Package.md) chapters.
