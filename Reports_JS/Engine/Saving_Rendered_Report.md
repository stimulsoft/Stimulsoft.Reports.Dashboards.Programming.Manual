# Saving Rendered Report

Rendered report can be saved into a **JSON** document for later viewing (data stored within a document):


**index.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("SimpleList.mrt");
report.renderAsync(function(){
    var jsonString = report.saveDocumentToJsonString();
});
...
```
