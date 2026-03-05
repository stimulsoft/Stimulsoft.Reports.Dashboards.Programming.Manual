# HTML5 Viewer

The report viewer is a Python component called `StiViewer`, designed for viewing, printing, and exporting reports in a browser window on any computer with any operating system. The viewer supports various themes, an animated interface, bookmarks, interactive reports, editing report elements on the page, full-screen mode, search, and other features essential for report viewing.


The viewer can display both the report template and an already generated report. If a report template is used, the viewer will automatically build it using the JavaScript report generator. Full support for working with interactive analytical dashboards is implemented. The functioning of the report generator is discussed in detail in the [Report Engine](../Engine/index.md) section.


The viewer's interface is built using HTML5, making it usable on virtually any modern platform. The component uses AJAX technology to perform all actions (loading and building reports, connecting to data, paging and zooming, interactivity in reports, printing, exporting, etc.), eliminating the need to reload the entire page and increasing performance, as well as enabling the component's use in single-page applications. The JavaScript technology used for building reports allows for use with virtually any low-performance server-side.

> **Information**
>
> Such as dashboards and reports use the same unified MRT template format, as well as the same methods for loading templates and working with data, the term "report" will be used throughout the documentation.

* [Deployment](Usage.md)
* [Working with Bookmarks](Work_with_Bookmark.md)
* [Activation](Activation.md)
* [Dynamic collapsing, sorting, and detailing](Interaction.md)
* [Showing Reports](Showing_Reports_and_Dashboards.md)
* [Editing Rendered Reports](Editable.md)
* [Localization](Localization.md)
* [Sending a report by Email](Send_Email.md)
* [Printing a Report](Printing_Report.md)
* [Invoking the Designer](Call_Designer.md)
* [Report Export](Export.md)
* [Visual Design](Using_Themes.md)
* [Display Modes](Mode_of_Show.md)
* [Viewer Events](Events.md)
* [Working with Report Variables](Work_with_Parameters.md)
* [Viewer Settings](Settings.md)
