# How this Works

To run the designer, you need to place the **StiMvcDesignerFx** component on the page, set the necessary properties and, if necessary, set the necessary actions on the view controller. When the report designer runs, the following actions occur:

* The .NET component generates HTML and JavaScript code that is necessary for displaying and running the designer;

* When the component is output, the client Flash application is launched. It requests a report on the server-side and displays it in the edit report window;

* Various actions, such as previewing a report, saving a report template, exporting a report, applying parameters, sorting and drill-down, cause certain actions on the server-side in which you can perform the necessary actions with the report.
