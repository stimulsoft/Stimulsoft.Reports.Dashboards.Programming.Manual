# Designer

> **Samples**
>
> On GitHub, you may find the samples which show how to work with the **Blazor Designer** component. We support [Blazor Server](https://github.com/stimulsoft/Samples-Blazor-Server) and [Blazor WebAssembly](https://github.com/stimulsoft/Samples-Blazor-WebAssembly). All the examples are separate projects, grouped into one solution for the Visual Studio.

The **Blazor Designer** component is designed to create reports in the web browser. And you don't need to set components or any special plugins on the client. All you need is a modern web browser. With the help of the **Blazor Designer**, you can create, edit, save, view reports, and print them on any computer with any installed operating system.


The **Blazor Designer** component is developed as a unique component, and it can work both with the Blazor Server and WebAssembly. When performing all actions on reports, the component requests only necessary data, which allows you to get rid of reloading the entire page and save Web traffic and increase work speed.


To use the **Blazor Designer** in a Web project, you should use the NuGet package [Stimulsoft.Reports.Blazor](https://www.nuget.org/packages/Stimulsoft.Reports.Blazor/) or [Stimulsoft.Dashboards.Blazor](https://www.nuget.org/packages/Stimulsoft.Dashboards.Blazor):

* Select the Manage NuGet Packages item in the context menu of the project;

* Specify the Stimulsoft.Reports.Blazor on the Browse in the search line;

* Select the element, define the package version, and click **Install**. You should click the **Update** when updating the package.


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
* [Additional Features of Preview](Additional_Functionality_of_Preview.md)
* [Editing Reports](Add_Designer.md)
* [Preview](Preview.md)
* [Creating New Reports](Creating_Report.md)
* [Localization](Localization.md)
* [Saving Reports](Save_Report.md)
* [Using Themes](Using_Themes.md)
* [Settings](Settings.md)
* [Designer Events](Events.md)
