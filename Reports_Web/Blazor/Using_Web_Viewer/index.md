# Viewer

> **Samples**
>
> Get acquainted with the examples of working with the **Blazor Viewer** component. The [Blazor Server](https://github.com/stimulsoft/Samples-Blazor-Server) and the [Blazor WebAssembly](https://github.com/stimulsoft/Samples-Blazor-WebAssembly) technologies are available on GitHub. All the samples are separate projects, grouped into one solution for Visual Studio.

The **Blazor Viewer** (**StiBlazorViewer**) component is intended for report viewing in the browser window. At the same time, you don't need to install components or some special plugins on the client. All you need is a modern Web browser. With the help of the **Blazor Viewer**, you can view, print, export reports on any computer with any installed operating system.


The **Blazor Viewer** component is developed as a universal component, and it can work both with the use of the **Blazor Server** and the use of the **WebAssembly** technology. When making all interactive actions on reports, the component requests only the necessary data; it allows to get rid of reloading the entire page, save Web traffic, and increase work speed.


The **Blazor Viewer** supports many design themes, animated interface, bookmarks, interactive reports, editing report elements on the page, full-screen mode, search, and other necessary report viewing features.


To use the **Blazor Viewer** in Web-project, you should install the Nuget package [Stimulsoft.Reports.Blazor](https://www.nuget.org/packages/Stimulsoft.Reports.Blazor/) or [Stimulsoft.Dashboards.Blazor](https://www.nuget.org/packages/Stimulsoft.Dashboards.Blazor):

* Select the «Manage Nuget Packages…» in the context project menu.

* Specify the Stimulsoft.Reports.Blazor, in the search line on the Browse tab;

* Select the element, define the version of a package, and click on the **Install**. When updating a package, you should click on the **Update**.


If for some reason it is not possible, you should add the following assemblies to the project:

Stimulsoft.Base.dll

Stimulsoft.Blockly.dll

Stimulsoft.Data.dll

Stimulsoft.Drawing.dll

Stimulsoft.Map.dll

Stimulsoft.Report.dll

Stimulsoft.Report.Blazor.dll

Stimulsoft.Report.Check.dll

Stimulsoft.Report.Helper.dll

Stimulsoft.Report.Web.dll

Stimulsoft.Report.WebDesign.dll

Stimulsoft.System.dll

Stimulsoft.System.Web.dll


You should additionally add the following assemblies to the project for using dashboards:
Stimulsoft.Dashboard.dll

Stimulsoft.Dashboard.Drawing.dll

Stimulsoft.Dashboard.Export.dll

* [Activation](Activation.md)
* [Dynamic Collapsing, Sorting, Drill-Down](Interaction.md)
* [Showing Report](Showing_Reports.md)
* [Work with Bookmarks](Work_with_Bookmarks.md)
* [Connecting Data](Connecting_Data.md)
* [Editing Report](Editable.md)
* [Localization](Localization.md)
* [Sending Report by Email](Send_Email.md)
* [Printing Reports](Printing_Reports.md)
* [Export and Printing from Code](Export_and_Print.md)
* [Exporting Reports](Export.md)
* [Basic Features](Main_Features.md)
* [Vieweing Modes](Mode_of_Show.md)
* [Viewer Events](Event.md)
* [Calling Designer from Viewer](Call_Designer.md)
* [Settings](Settings.md)
* [Work with parameters](Work_with_Parameters.md)
