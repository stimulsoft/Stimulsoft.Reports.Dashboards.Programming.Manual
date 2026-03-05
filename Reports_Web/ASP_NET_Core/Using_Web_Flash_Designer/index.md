# Flash Designer

> **YouTube** [for the .NET Core Flash Designer](https://www.youtube.com/watch?v=SvKzg9viYzc&index=12&list=PL-72PPAq-3SX80j_FIJAcNppiQcOMyGpK)


> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-NET.Core-MVC-CSharp) examples for working with the .NET Core Flash Designer component. All examples are separate projects, grouped into one solution for Visual Studio.

The **Flash Designer** component (**StiNetCoreDesignerFx**) is designed to edit reports in the browser window. You do not need to install the .NET Framework, ActiveX components or any special plug-ins from the client. All you need is a Web browser with Flash support.


With **Flash Designer**, you can create, edit, save, view and print reports on any computer with any installed operating system, where there is an Internet connection and a Web browser with Flash support.


**Flash Designer** is divided into two parts - client and server. The client-side is the graphics wrapper of the designer, implemented using the Flash technology. The report engine built using the .NET Core technology is used to render reports. This is a cross-platform technology. It allows you to deploy the application on servers that use the operating systems like Windows, macOS, and Linux. Also, the server-side contains modules that perform the functions of receiving requests, processing them, and then transferring the linked data to the client-side. These two parts are assembled into one library and presented as an .NET Core component.


To use the **Flash Viewer** in a Web project, you need to install the NuGet package of [Stimulsoft.Reports.Web.NetCore](https://www.nuget.org/packages/Stimulsoft.Reports.Web.NetCore):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Reports.Web.NetCore in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.

* [How this Works?](How_It_Work.md)
* [Preview](Preview.md)
* [Editing Reports](Editting_Report.md)
* [Additional Features of Preview](Additional_Functionality_of_Preview.md)
* [Creating New Reports](Creating_Report.md)
* [Additional Features of Designer](Additional_Features_of_Designer.md)
* [Saving Reports](Saving_Report.md)
* [Additional Methods](Additional_Methods.md)
* [Localization](Localization.md)
* [Caching](Cashing.md)
* [Designer Settings](Settings.md)
