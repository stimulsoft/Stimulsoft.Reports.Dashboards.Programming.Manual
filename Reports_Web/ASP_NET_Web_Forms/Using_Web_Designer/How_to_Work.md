# How this Works

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To run the designer, you need to place the **StiWebDesigner** component on the ASPX page, set the necessary properties, and, if necessary, set the necessary event handlers. When the report designer runs, the following actions occur:

* The .NET component generates HTML and JavaScript code that is necessary for displaying and running the designer;

* When the component is output, the JavaScript method is launched. It requests the report template on the server side displays it in the designer window;

* Various actions in the designer (for example, report preview, saving the report template, export reports, sorting, drill-down, etc.) call a particular action on the server-side. You can perform the necessary manipulations with the report.
