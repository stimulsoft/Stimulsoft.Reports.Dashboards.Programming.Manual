# Vanilla JavaScript

This part describes an example of quickly deploying Stimulsoft in pure JavaScript applications. This application consists of an HTML page and JS scripts.

### Create an index.html file

This can be any HTML file, but by default, the entry point is `index.html`.


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

**Install Stimulsoft components**

First, you need to download the Stimulsoft package. If you need reporting tools, you should download the [Stimulsoft Reports.JS](https://www.stimulsoft.com/ru/downloads#reports) package. If you need reporting tools and dashboards, you should download the [Stimulsoft Dashboards.JS](https://www.stimulsoft.com/ru/downloads#dashboards) package. Then, you should connect the Stimulsoft scripts in the `index.html` file.


**index.html

          ...
          <script type="text/javascript" src="scripts/stimulsoft.reports.js"></script>
          <script type="text/javascript" src="scripts/stimulsoft.dashboards.js"></script>
          <script type="text/javascript" src="scripts/stimulsoft.designer.js"></script>
          <script type="text/javascript" src="scripts/stimulsoft.viewer.js"></script>
          <script type="text/javascript" src="scripts/stimulsoft.blockly.editor.js"></script>
          ...**

**Create a start function**
For example, create a function to open the report designer with an empty report.


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

Alternatively, create a function to open the report viewer with a previously created report template.


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

### First Start

By default, the browser doesn’t have access to the file system due to the browser's security policy. To ensure the local project runs correctly, you should use a web server. For example, you can globally install [http-server](https://www.npmjs.com/package/http-server) or [serve](https://www.npmjs.com/package/serve), and then start the web server from the command line in the project's root folder. In this case, `index.html` will be opened in the browser with the Stimulsoft designer or viewer.
