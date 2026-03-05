# HTML5 Designer

> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-NET-6.0-Razor-CSharp) examples of working with the ASP.NET Core Razor HTML5 Designer component. All examples are separate projects, grouped into one solution for Visual Studio.

The **HTML5 Designer** (**StiNetCoreDesigner**) component is designed to create reports in the web browser. You do not need to install the .NET Framework, ActiveX components or any special plug-ins on the client side. All that is needed is any modern Web browser.


With help of **HTML5 Designer** you can create, edit, save and preview reports on any computer with any operating system installed. Since the designer only uses HTML and JavaScript technologies, it can be run on devices where there is no Flash or Silverlight support - tablets, smartphones. Also, the designer supports the Touch interface, which is automatically enabled when using devices with a touch screen.


The **HTML5 Designer** component uses the AJAX technology to perform all actions on reports, which allows you to get rid of reloading the entire page, save Web traffic and speed up work. The report engine built using the .NET Core technology is used to render reports. This is a cross-platform technology. It allows you to deploy the application on servers that use the operating systems like Windows, macOS, and Linux.


> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To use the **HTML5 Designer** in a Web project, you need to install the NuGet package of [Stimulsoft.Reports.Web.NetCore](https://www.nuget.org/packages/Stimulsoft.Reports.Web.NetCore):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Reports.Web.NetCore in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.


To add the ability to create and edit dashboards in a Web project, install the NuGet package [Stimulsoft.Dashboards.Web.NetCore](https://www.nuget.org/packages/Stimulsoft.Dashboards.Web.NetCore/) (this package is associated with the package Stimulsoft.Reports.Web.NetCore. If it is missed it will be installed automatically):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Dashboards.Web.NetCore in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.

* [How this Works?](How_It_Works.md)
* [Additional Features of Preview](Additional_Functionality_of_Preview.md)
* [Activation](Activation.md)
* [Timeout](Timeout.md)
* [Editing Reports and Dashboards](Add_Designer.md)
* [Localization](Localization.md)
* [Creating New Reports and New Dashboards](Creating_Report.md)
* [Using Themes](Using_Themes.md)
* [Saving Reports and Dashboards](Save_Report.md)
* [Caching](Caching.md)
* [Preview](Preview.md)
* [Additional Methods](Events.md)
* [Settings](Settings.md)
