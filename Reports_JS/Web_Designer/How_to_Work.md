# How this Works

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **StiDesigner** component is developed using only HTML5 and JavaScript technology, and does not require a server for its work (it is necessary only for hosting project files). When you run the report viewer, the following actions occur:

* The JavaScript component adds designer interface code to the current HTML page;

* If a report object is assigned, the report will be uploaded to the designer page to edit it;

* Each action in the designer (for example, report preview, saving a report template, exporting a report, applying parameters, sorting and detailing a report) calls a specific JavaScript event in which you can perform the necessary manipulations with the report.
