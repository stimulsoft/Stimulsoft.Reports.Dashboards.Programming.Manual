# How this Works

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To run the designer, you need to place the **StiNetCoreDesigner** component on the page, set the necessary settings to it, and set the necessary actions in the view controller. When the report designer runs, the following actions occur:

* The .NET Core component generates HTML and JavaScript code that is necessary for displaying and running the designer;

* When the component is output, the JavaScript method is launched. It requests the report template on the server side displays it in the designer window;

* Various actions in the designer (for example, report preview, saving the report template, export reports, sorting, drill-down etc.) calls a certain action on the server side, in which you can perform the necessary manipulations with the report.
