# Step by Step for Node.js

This example shows how to install and run Stimulsoft JS for Node.js. Also, you can find more samples [Reports for Node.js](https://github.com/stimulsoft/Samples-Reports.JS-for-Node.js/tree/master) and [Dashboards for Node.js](https://github.com/stimulsoft/Samples-Dashboards.JS-for-Node.js/tree/master) on the GitHub.

**Step 1**: Create a folder;


**Step 2**: Add a report template in this folder;


**Step 3**: Create **index.js** file in this folder;


**Step 4**: Open console;


**Step 5**: [Install the Reports.JS module in this folder](https://www.npmjs.com/package/stimulsoft-reports-js):


| **console** |
| --- |
| npm install stimulsoft-reports-js |

Or


[Install the Dashboards.JS module in this folder:](https://www.npmjs.com/package/stimulsoft-dashboards-js)


| **console** |
| --- |
| npm install stimulsoft-dashboards-js |

**Step 6**: Open **index.js** file in the editor;


**Step 7**: Add the required code.


**index.js**

```javascript
...
// Stimulsoft reports module loading
var Stimulsoft = require('stimulsoft-reports-js');

// Loading fonts
Stimulsoft.Base.StiFontCollection.addOpentypeFontFile("Roboto-Black.ttf");

//Creating a new report object
var report = Stimulsoft.Report.StiReport.createNewReport();

// Load report template in the report object
report.loadFile("report1.mrt");

// Save report object in mrt file
report.saveFile("report2.mrt");
...
```

**Step 8**: Save changes in the **index.js** file;


**Step 9**: Open console and run **index.js**.


| **console** |
| --- |
| node index |

**Step 10**: You can perform various actions on reports with using **Node.js**. For example, let's export the report to pdf. Open **index.js** in the editor, define this code and save changes.


**index.js**

```javascript
...
// Stimulsoft Reports module
var Stimulsoft = require('stimulsoft-reports-js');

// Loading fonts
Stimulsoft.Base.StiFontCollection.addOpentypeFontFile("Roboto-Black.ttf");

// Creating new report
var report = new Stimulsoft.Report.StiReport();

// Loading report template
report.loadFile("report1.mrt");

// Renreding report
report.renderAsync(() => {
    console.log("Report rendered. Pages count: ", report.renderedPages.count);
    
    // Export to PDF
    report.exportDocumentAsync((pdfData) => {
        
        // Converting Array into buffer
        var buffer = Buffer.from(pdfData)
        
        // File System module
        var fs = require('fs');
        
        // Saving string with rendered report in PDF into a file
        fs.writeFileSync('./SimpleList.pdf', buffer);
        console.log("Rendered report saved into PDF-file.");
    }, 
    Stimulsoft.Report.StiExportFormat.Pdf);
});
...
```

**Step 11**: Open console and run **index.js**.


| **console** |
| --- |
| node index |
