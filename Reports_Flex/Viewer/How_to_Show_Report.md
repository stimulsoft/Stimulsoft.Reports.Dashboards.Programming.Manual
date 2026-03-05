# How to Show Report

Put the **Viewer.Fx** on the scene of a **Flex** application:


**Code**

```
...
<viewer:StiViewerFx id="viewerFx" Left="0" right="0" bottom="0" />
...
```

Create, load and assign a report:


**Code**

```
...
var report: StiReport = new StiReport();
report.loadDocumentFromString(documentString);
viewerFx.report = report;
...
```


> **Information**
>
> documentString: String - .mdc file loaded as a string.

Also, there is another way to show a report instead of placing **Viewer.Fx** on the scene of a Flex application:


**Code**

```
...
var report: StiReport = new StiReport();
report.loadDocumentFromString(documentString);
report.showDialog();
...
```


> **Information**
>
> report.show() - showing ViewerFx on the working space of the application.
