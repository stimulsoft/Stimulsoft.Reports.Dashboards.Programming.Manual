# Flash Viewer

> **YouTube** [for the ASP.NET MVC Flash Viewer](https://www.youtube.com/watch?v=SvKzg9viYzc&index=12&list=PL-72PPAq-3SX80j_FIJAcNppiQcOMyGpK)


> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-ASP.NET-MVC-CSharp) examples for working with the ASP.NET MVC Flash Viewer component. All examples are separate projects, grouped into one solution for Visual Studio.

The **Flash Viewer (****StiMvcViewerFx****)** component is designed to view reports in the web browser. You do not need to install the .NET Framework, ActiveX components or any special plug-ins on the client-side. All that is needed a Web browser with Flash support.


With help of **Flash Viewer**, you can view, print and export reports on any computer with any installed operating system, where there is an Internet connection and a Web browser with Flash support.


**Flash Viewer** is divided into two parts - client and server. The client-side is the graphics wrapper of the viewer, implemented using the Flash technology. The server-side is the report engine that uses the .NET Framework to render reports. Also, the server-side contains modules that perform the functions of receiving requests, processing them, and then transferring the linked data to the client-side. These two parts are assembled into one library and presented as an ASP.NET MVC component.


**Flash Viewer** supports many themes, animated interface, bookmarks, interactive reports, editing of report elements on the page, full screen mode, and other necessary features for viewing reports. Its distinctive feature is the speed of work and the same appearance of both the viewer itself, and viewed reports on any computer with any installed operating system.


To use the **Flash Viewer** in a Web project, you need to install the NuGet package of [Stimulsoft.Reports.Web](https://www.nuget.org/packages/Stimulsoft.Reports.Web):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Reports.Web in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.


If this is not possible, you should add the following assemblies to the project:

* Stimulsoft.Base.dll

* Stimulsoft.Report.dll

* Stimulsoft.Report.Check.dll

* Stimulsoft.Report.Helper.dll

* Stimulsoft.Report.Mvc.dll

* Stimulsoft.Report.Web.dll

* Stimulsoft.Report.WebDesign.dll

* [How this Works?](How_to_Work.md)
* [Interactive Reports](Interaction.md)
* [Showing Reports](Showing_Report.md)
* [Work with Parameters](Work_with_Parameters.md)
* [Connecting Data](Connecting_Data.md)
* [Sending Report by email](Send_Email.md)
* [Localization](Localization.md)
* [Calling Designer and Viewer](Call_Designer.md)
* [Printing Reports](Printing_Report.md)
* [Using Themes](Using_Themes.md)
* [Export Reports](Export_Setting.md)
* [Additional Methods](Export_Report_from_Code.md)
* [Work with Bookmarks](Work_with_Bookmarks.md)
* [Viewer Settings](Settings.md)
