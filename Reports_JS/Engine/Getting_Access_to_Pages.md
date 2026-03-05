# Getting Access to Pages

### Getting access to pages of a report

The report has a collection of pages, which can be accessed by the following way:


**index.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("SimpleList.mrt");

for (var index = 0; index < report.pages.count; index++) {
    alert(report.pages.getByIndex(index).name);
}
...
```

### Getting access to pages of a rendered report

After rendering the report, a collection of pages is created. It can be accessed by the following way:


**index.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("SimpleList.mrt");
report.renderAsync(function(){
    for (var index = 0; index < report.renderedPages.count; index++) {
        alert(report.renderedPages.getByIndex(index).name);
    }
});
...
```
