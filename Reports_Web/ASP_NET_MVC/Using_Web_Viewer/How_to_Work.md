# How this Works

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To run the viewer, you need to place the **StiMvcViewer** component on the page, set the necessary settings, and set the necessary actions in the view controller. When the report viewer runs, the following actions occur:

* The .NET component generates HTML and JavaScript code that is necessary for displaying and running the viewer;

* When the component is output, the JavaScript method is launched. It requests the first page of the report on the server-side or the entire report (depending on the selected mode) and the required report parameters;

* Each action in the viewer (for example, paging, printing or exporting a report, etc.) calls a certain action on the server-side, in which you can perform the necessary manipulations with the report;

* To speed up the work, the viewer saves the report in cache or server session, which makes it impossible to re-build the report.
