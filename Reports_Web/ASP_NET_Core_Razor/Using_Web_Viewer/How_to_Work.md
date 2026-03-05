# How this Works

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To run the viewer, you should place the **StiNetCoreViewer** component on a page, set the necessary properties, and define necessary actions in the page event handler. When running the report viewer, the following actions occur:

* The .NET Core component generates HTML and JavaScript code that is necessary for displaying and running the viewer;

* When the component is output, the JavaScript method is launched. It requests the first page of the report on the server-side or the entire report (depending on the selected mode) and the required report parameters;

* Each action in the viewer (for example, paging, printing or exporting a report, etc.) calls a certain action on the server-side, in which you can perform the necessary manipulations with the report;

* The viewer saves the report in cache or server session to speed up the work, which makes it impossible to re-build the report.
