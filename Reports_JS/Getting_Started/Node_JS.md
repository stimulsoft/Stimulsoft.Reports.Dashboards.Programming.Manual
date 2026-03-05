# Node JS

This part describes an example of using Stimulsoft in Node.js applications. In this case, you can use only the report engine without the visual components, such as the report designer and viewer.


**Create a Node.js project**
In the terminal, navigate to the directory where you want to place the new project. Then, run the following command.


**terminal**

npm init

The application settings can be left at default or modified as needed.

**Install Stimulsoft components**

First, you need to download the Stimulsoft package. If you need reporting tools, you should download the [Stimulsoft Reports.JS](https://www.stimulsoft.com/ru/downloads#reports) package. If you need reporting tools and dashboards, you should download the [Stimulsoft Dashboards.JS](https://www.stimulsoft.com/ru/downloads#dashboards) package. For this, run the following command.

**terminal**

npm install stimulsoft-dashboards-js

**Create a file project**
This can be any js file, for example `index.js`.

**Add reports to the project**
Copy the folder with **reports** to the project. For example, the reports folder will contain the report file **Invoice.mrt**.

**Integrate Stimulsoft into the application**
To do this, edit the `index.js` file in the project's folder. First, you need to import the Stimulsoft module. Then, create a `StiReport()` object, load the report into it, build it and export it as a PDF file.


**index.js**

```javascript

var Stimulsoft = require("stimulsoft-dashboards-js");

var report = new Stimulsoft.Report.StiReport();
report.loadFile("reports/Invoice.mrt");

report.renderAsync(function () {
    report.exportDocumentAsync(function (data) {
        var buffer = new Buffer.from(data, "utf-8");
        var fs = require("fs");
        fs.writeFileSync("Invoice.pdf", buffer);
    }, Stimulsoft.Report.StiExportFormat.Pdf);
});
```

**First Start**
To do this, run the project file in the Node.js


**console**

node index.js
