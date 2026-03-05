# Loading and Saving Report

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

Two methods of the **StiReport** object are used to load a report – **loadFile()** and **load()**. They are used as follows:

  * loadFile(filePath) – loads a report from the **MRT** file which path is specified in the filePath;

  * load(str) – loads a report from the string str, that contains **XML** or **JSON**;

  * load(data) – loads a report from the **array data** of the number[] type;

  * load(xml) – loads a report from the XML of the **XMLDocument** type;

  * load(json) – loads a report from the **JS** object.


For example, use the code below to load a report from file:


**index.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("SimpleList.mrt");
...
```

The **MRT** format of Stimulsoft Reports is the **JSON** based description of reports. You can use **MRT** files, created in other Stimulsoft Reports designers in the **JSON** based description. Use the code below to save a report to a string:


**index.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
var jsonString = report.saveToJsonString();
...
```

Use the code below to load a report from this string:


**index.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.load(jsonString);
...
```
