# Scripts of Reports.JS Package

**Reports.JS** package contains the following scripts:


| **Scripts** | **Description** |
| --- | --- |
| **Common Scripts *:** |  |
| **stimulsoft.blockly.editor.js** | The script contains visual editor Blockly for creating event scripts in a report. The Event handler is embedded in report engine. |
| **stimulsoft.designer.js** | The script for working with the report designer. |
| **stimulsoft.reports.js** | The main script contains all the functionality of the report generator - rendering, exporting, working with data. |
| **stimulsoft.reports.maps.js** | The script contains resources for working with region maps. |
| **stimulsoft.viewer.js** | The script for working with the report viewer. |
| stimulosft.reports.js can be split into *: |  |
| **stimulsoft.reports.engine.js** | The main script of the report generator. |
| **stimulsoft.reports.chart.js** | The script is necessary for working with charts. |
| **stimulsoft.reports.export.js** | The script is necessary for exporting reports. |
| **stimulsoft.reports.import.xlsx.js** | The script is necessary for importing data from XLSX files. |
| Other Files: |  |
| **stimulsoft.reports.d.ts** | The header file describes the syntax and structure of functions and properties. |

* - Also, you can use packed scripts instead of common scripts or parts of the stimulsoft.reports.js. Packed scripts allow you to reduce the script file size by several times. The names of packed scripts correspond with the names of scripts, but they contain the word **pack** in the name before the **js** extension. For example, a packed analog of the **stimulsoft.reports.js** script will be the **stimulsoft.reports.pack.js**.
