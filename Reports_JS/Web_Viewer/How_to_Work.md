# How this Works

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **StiViewer** component is designed to use only HTML5 and JavaScript technology, and does not require a server for its work (it is necessary only for hosting project files). When you run the report viewer, the following actions occur:

* JavaScript component adds code of the viewer interface to the current HTML page;

* If a report object has been assigned, the report will be rendered, then, the first page of the report will be displayed;

* Each action in the viewer (for example, paging, printing or exporting a report, etc.) calls a specific JavaScript event in which you can perform the necessary manipulations with the server report, which eliminates the re-build of the report.
