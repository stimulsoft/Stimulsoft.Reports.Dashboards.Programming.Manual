# HTML5 Designer

> **YouTube**
>
> Watch videos [for working with JS HTML5 Designer](https://www.youtube.com/watch?v=vqbZz0ythKc&list=PL-72PPAq-3SVanYQ9GVxG6TBITDcveRXx&index=7). Subscribe to the [Stimulsoft channel](https://www.youtube.com/user/StimulsoftVideos) to watch new video lessons. Leave your questions and suggestions in the comments to the video.


> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-JS) examples of working with the JS HTML5 Designer component. All samples are separate projects, grouped into one solution.

The **HTML5 Designer** (**StiDesigner**) component is designed to create reports in the web browser. You do not need to install the .NET Framework, ActiveX components or any special plug-ins on the client side. All that is needed is any modern Web browser.


With help of **HTML5 Designer** you can create, edit, save and preview reports on any computer with any operating system installed. Since the designer uses only HTML and JavaScript technologies, it can be run on devices where there is no Flash or Silverlight support - tablets, smartphones. Also, the designer supports the Touch interface, which is automatically enabled when using devices with a touch screen.


The **HTML5 Designer** component uses the **JavaScript** technology to perform all actions on reports, which allows you to get rid of reloading the entire page and speed up work.


> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To use the **HTML5 Designer** in projects, you need to install the npm package of [stimulsoft-reports-js](https://www.npmjs.com/package/stimulsoft-reports-js):
npm install stimulsoft-reports-js

If this is not possible, you should add the following scripts to the project.


**designer.html**

```html
...
<script src="scripts/stimulsoft.report.js"></script>
<script scr="scripts/stimulsoft.viewer.js"></script>
<script src="scripts/stimulsoft.designer.js"></script>

<!-- Stimulsoft Blockly editor for JS Designer -->
<script src="scripts/stimulsoft.blockly.editor.js"></script>
...
```

Install the npm package to use the HTML5 Viewer in a project to view reports and dashboards [stimulsoft-dashboards-js](https://www.npmjs.com/package/stimulsoft-dashboards-js):

npm install stimulsoft-dashboards-js


If this is not possible, you should add the following scripts to the project.


**viewer.html**

```html
...
<script src="scripts/stimulsoft.report.js"></script>
<script src="scripts/stimulsoft.dashboards.js"></script>
<script scr="scripts/stimulsoft.viewer.js"></script>
<script src="scripts/stimulsoft.designer.js"></script>
...
```


> **Information**
>
> The script variants that you can use in your projects can be found in the [Scripts of Reports.JS Package](../../Deployment/Files_in_Reports_JS_Package.md) and [Scripts of Dashboards.JS Package](../../Deployment/Scripts_in_Dashboards_JS_Package.md) chapters.
