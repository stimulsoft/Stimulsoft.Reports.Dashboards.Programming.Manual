# Vanilla JavaScript and CDN Services

This chapter will cover an example of quickly deploying Stimulsoft in pure JavaScript applications by connecting script files via CDN services. Such an application consists of an HTML page and links to JS scripts.

### Create an index.html file

It can be any HTML file, but by default, the entry point is considered to be `index.html`.


**index.html

          <!DOCTYPE html>
          <html lang="en">
          <head>
              <meta charset="UTF-8">
              <meta name="viewport" content="width=device-width, initial-scale=1.0">
              <title>Document</title>
          </head>
          <body>
             
          </body>
          </html>**

### Connect stimulsoft script files

Currently, the following services can be used:

- [cdn.jsdelivr.net](https://cdn.jsdelivr.net/npm/stimulsoft-reports-js/Scripts/stimulsoft.reports.js);
- [unpkg.com](https://www.unpkg.com/stimulsoft-reports-js/Scripts).


These services provide access to script files via URLs from the [npm](https://www.npmjs.com/search?q=stimulsoft) packages [stimulsoft-reports-js](https://www.npmjs.com/package/stimulsoft-reports-js) and [stimulsoft-dashboards-js](https://www.npmjs.com/package/stimulsoft-dashboards-js). This allows you to include script files in your `index.html` file via their URLs. For example, using the `cdn.jsdelivr.net` service:


**index.html

          ...
          <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/stimulsoft-reports-js/Scripts/stimulsoft.reports.js"></script>
          <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/stimulsoft-reports-js/Scripts/stimulsoft.designer.js"></script>
          <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/stimulsoft-reports-js/Scripts/stimulsoft.viewer.js"></script>
          <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/stimulsoft-reports-js/Scripts/stimulsoft.blockly.editor.js"></script>
          ...**

Or, using the `unpkg.com` service:


**index.html

          ...
          <script type="text/javascript" src="https://www.unpkg.com/stimulsoft-dashboards-js/Scripts/stimulsoft.reports.js"></script>
          <script type="text/javascript" src="https://www.unpkg.com/stimulsoft-dashboards-js/Scripts/stimulsoft.dashboards.js"></script>
          <script type="text/javascript" src="https://www.unpkg.com/stimulsoft-dashboards-js/Scripts/stimulsoft.designer.js"></script>
          <script type="text/javascript" src="https://www.unpkg.com/stimulsoft-dashboards-js/Scripts/stimulsoft.viewer.js"></script>
          <script type="text/javascript" src="https://www.unpkg.com/stimulsoft-dashboards-js/Scripts/stimulsoft.blockly.editor.js"></script>
          ...**


> **Information**
>
> Please note that using the `cdn.jsdelivr.net` and `unpkg.com` services, you can include various scripts provided in the [stimulsoft-reports-js](https://www.npmjs.com/package/stimulsoft-reports-js) and [stimulsoft-dashboards-js](https://www.npmjs.com/package/stimulsoft-dashboards-js) packages. Additionally, you can include script files of a specific npm package version by specifying it in the URL with the `@` symbol. For example, [https://cdn.jsdelivr.net/npm/stimulsoft-reports-js@2024.4.1/Scripts/stimulsoft.reports.js](https://cdn.jsdelivr.net/npm/stimulsoft-reports-js@2024.4.4/Scripts/stimulsoft.reports.js) или [https://www.unpkg.com/stimulsoft-reports-js@2024.4.1/Scripts/stimulsoft.reports.js](https://www.unpkg.com/stimulsoft-reports-js@2024.4.4/Scripts/stimulsoft.reports.js).
>
>
> If the version isn't specified in the URL, the script files will be loaded from the latest available version of the [stimulsoft-reports-js](https://www.npmjs.com/package/stimulsoft-reports-js)  or [stimulsoft-dashboards-js](https://www.npmjs.com/package/stimulsoft-dashboards-js) package.

### Create a launch function

For example, a function to launch the report designer with an empty report.


**index.html

          ...
          <script type="text/javascript">
          function onLoad() {
          var report = new Stimulsoft.Report.StiReport();
          
          var designer = new Stimulsoft.Designer.StiDesigner();
          designer.renderHtml('content');
          designer.report = report;
          }
          </script>
          
          ...
          
          <body onload="onLoad()">
          <div id="content"></div>
          </body>
          ...**

Or, a function to launch the report viewer with a previously created report template.


**index.html

          ...
          <script type="text/javascript">
          function onLoad() {
          var report = new Stimulsoft.Report.StiReport();
          report.loadFile('reports/Report.mrt');
          
          var viewer = new Stimulsoft.Viewer.StiViewer();
          viewer.renderHtml('content');
          viewer.report = report;
          }
          </script>
          
          ...
          
          <body onload="onLoad()">
          <div id="content"></div>
          </body>
          ...**

### First launch

By default, browsers do not have access to the file system due to browser security policies. To ensure that a local project runs correctly, you need to use web servers. For example, you can globally install [http-server](https://www.npmjs.com/package/http-server) or [serve](https://www.npmjs.com/package/serve) and then start a web server from the command line in the root folder of the project. In this case, the `index.html` file will open in the browser with the Stimulsoft designer or viewer.
