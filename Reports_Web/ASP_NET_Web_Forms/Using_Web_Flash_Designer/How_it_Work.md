# How this Works

To run the designer, you need to put the **StiWebDesignerFx** component on the page, set the necessary settings to it, and set the necessary event handlers. When you run the report designer, the following actions occur:

* The .NET component generates HTML and JavaScript code, necessary for displaying and working with the report designer;

* When the component is output, the client Flash application is launched. It requests a report template on the server-side and displays it in the window;

* Various actions, such as previewing a report, saving a report template, exporting a report, applying parameters, sorting and drill-down in reports, cause a certain action on the server-side in which you can perform the necessary manipulations with the report.
