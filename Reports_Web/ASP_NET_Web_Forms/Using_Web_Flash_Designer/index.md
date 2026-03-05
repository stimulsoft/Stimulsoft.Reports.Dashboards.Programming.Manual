# Flash Designer

> **YouTube** [for the ASP.NET Flash Designer](https://www.youtube.com/watch?v=fSA1j1-8yNQ&list=PL-72PPAq-3SUmzS9elmeG-Uo3cRyJWmn0)


> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-ASP.NET-CSharp) examples for working with the ASP.NET Flash Designer component. All examples are separate projects, grouped into one solution for Visual Studio.

The **Flash Designer** component (**StiWebDesignerFx**) is designed to edit reports in the browser window. You do not need to install the .NET Framework, ActiveX components or any special plug-ins from the client. All you need is a Web browser with Flash support.


With **Flash Designer**, you can create, edit, save, view and print reports on any computer with any installed operating system, where there is an Internet connection and a Web browser with Flash support.


**Flash Designer** is divided into two parts - client and server. The client-side is the graphics wrapper of the designer, implemented using the Flash technology. The server-side is the report engine that uses the .NET Framework to render reports. Also, the server-side contains modules that perform the functions of receiving requests, processing them, and then transferring the linked data to the client-side. These two parts are assembled into one library and presented as an ASP.NET component.


In order to use **Flash Designer** in a Web-project, the installation of the [Stimulsoft.Reports.Web](https://www.nuget.org/packages/Stimulsoft.Reports.Web) NuGet package is required:

* Select 'Manage NuGet Packages...' menu item in the project's pop-up menu;

* In the 'Browse' tab, type 'Stimulsoft.Reports.Web' in the search textbox;

* Click the Stimulsoft.Report.Web package, select the version of the package and click **Install**. If the package should be updated, use the **Update** button.


If, for some reason, that is not possible, the following assemblies should be added to the project:
* Stimulsoft.Base.dll

* Stimulsoft.Report.dll

* Stimulsoft.Report.Check.dll

* Stimulsoft.Report.Helper.dll

* Stimulsoft.Report.Web.dll

* Stimulsoft.Report.WebDesign.dll

* [How this Works?](How_it_Work.md)
* [Preview](Preview.md)
* [Editing Reports](Editing_Report.md)
* [Additional Features of Preview](Additional_Functionality_of_Preview.md)
* [Creating New Reports](Creating_Report.md)
* [Localization](Localization.md)
* [Saving Reports](Save_Report.md)
* [Additional Features of Designer](Additional_Functionality_of_Designer.md)
* [Caching](Cashing.md)
* [Designer Events](Event.md)
* [Settings](Settings.md)
