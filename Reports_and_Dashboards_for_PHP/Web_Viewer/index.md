# HTML5 Viewer

The report viewer is a PHP component (`StiViewer`) designed for viewing, printing, and exporting reports and dashboards in a browser window on any computer, regardless of the operating system. The viewer supports various themes, an animated interface, bookmarks, interactive reports, in-page editing of report elements, full-screen mode, search functionality, and other essential features for report viewing.


The viewer can display a report template, a built report, or a dashboard. If a report template is used, the viewer will automatically build it using the JavaScript report generator. The operation of the generator is discussed in more detail in the  [Engine](../Engine/index.md) section.


The viewer's interface is built using HTML5, allowing it to run on almost any modern platform. The component utilizes AJAX technology to perform all actions (loading and building the report, connecting to data, page navigation and scaling, interactivity in reports, printing, exporting, etc.), eliminating the need to reload the entire page, thus improving performance and making it suitable for use in one-page applications. The JavaScript technology used for report building enables the use of virtually any server-side, even with low performance.


> **Information**
>
> Since both dashboards and reports use the same unified MRT template format, as well as methods for loading templates and working with data, the term "report" will be used in the documentation.

* [Deployment](Usage.md)
* [Work with Bookmarks](Work_with_Bookmark.md)
* [Activation](Activation.md)
* [Dynamic Sorting, Collapsing, and Drill-Down](Interaction.md)
* [Showing Reports and Dashboards](Showing_Reports_and_Dashboards.md)
* [Editing Report](Editable.md)
* [Localization](Localization.md)
* [Sending Report By Email](Send_Email.md)
* [Printing Report](Printing_Report.md)
* [Calling Designer from Viewer](Call_Designer.md)
* [Report Export](Export.md)
* [Appearance](Using_Themes.md)
* [Viewing Modes](Mode_of_Show.md)
* [Viewer Events](Events.md)
* [Work with Report Variables](Work_with_Parameters.md)
* [Viewer Settings](../Settings.md)
