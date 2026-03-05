# How this Works

To run the viewer, you need to place the **StiNetCoreViewerFx** component on the ASPX page, set the necessary properties and, if necessary, set the necessary event handlers. When the report viewer runs, the following actions occur:

* The .NET Core component generates HTML and JavaScript code that is necessary for displaying and running the viewer;

* When the component is output, the client Flash application is launched. It requests a report on the server-side (if necessary, the report is rendered), and displays it;

* Interactive actions, such as exporting a report, applying parameters, sorting and report drill-down, call a certain action on the server-side, in which you can perform the necessary manipulations with the report.
