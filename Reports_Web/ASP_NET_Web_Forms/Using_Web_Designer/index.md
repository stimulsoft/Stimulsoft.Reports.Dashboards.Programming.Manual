# HTML5 Designer

> **YouTube**
>
> Watch videos [for working with ASP.NET HTML5 Designer](https://www.youtube.com/watch?v=fSA1j1-8yNQ&list=PL-72PPAq-3SUmzS9elmeG-Uo3cRyJWmn0). Subscribe to the [Stimulsoft channel](https://www.youtube.com/user/StimulsoftVideos) to find out about the new video lessons uploaded. Leave your questions and suggestions in the comments to the video.


> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-ASP.NET-CSharp) examples of working with the ASP.NET HTML5 Designer component. All samples are separate projects grouped into one solution for Visual Studio.

The **HTML5 Designer (StiWebDesigner)** component is designed to create reports in the web browser. You do not need to install the .NET Framework, ActiveX components, or any special plug-ins on the client-side. All you need is any modern Web browser.


With the help of **HTML5 Designer**, you can create, edit, save and preview reports on any computer with any operating system installed. Since the designer only uses HTML and JavaScript technologies, it can be run on devices without Flash or Silverlight support - tablets, smartphones. Also, the designer supports the Touch interface, which is automatically enabled when using devices with a touch screen.


The **HTML5 Designer** component uses the AJAX technology to perform all actions on reports, which allows you to get rid of reloading the entire page, save Web traffic, and speed up work.

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To use **HTML5 Designer** in a Web-project, the installation of the [Stimulsoft.Reports.Web](https://www.nuget.org/packages/Stimulsoft.Reports.Web) NuGet package is required:

* Select 'Manage NuGet Packages...' menu item in the project's pop-up menu;

* In the 'Browse' tab, type 'Stimulsoft.Reports.Web' in the search textbox;

* Click the Stimulsoft.Report.Web package, select the version of the package, and click **Install**. If the package should be updated, use the **Update** button.


If for some reason, that is not possible, the following assemblies should be added to the project:
* Stimulsoft.Base.dll

* Stimulsoft.Report.dll

* Stimulsoft.Report.Check.dll

* Stimulsoft.Report.Helper.dll

* Stimulsoft.Report.Web.dll

* Stimulsoft.Report.WebDesign.dll


To add the ability to create and edit dashboards in a Web project, install the NuGet package [Stimulsoft.Dashboards.Web](https://www.nuget.org/packages/Stimulsoft.Dashboards.Web/) (this package is associated with the package Stimulsoft.Reports.Web. If it is missed, it will be installed automatically):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Dashboards.Web in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.


If for some reason this is not possible, you should additionally add the following assemblies to the project:
* Stimulsoft.Dashboard.dll

* Stimulsoft.Dashboard.Drawing.dll
* Stimulsoft.Dashboard.Export.dll

* [How this Works?](How_to_Work.md)
* [Additional Functionality of Preview](Additional_Functionality_of_Preview.md)
* [Activation](Activation.md)
* [Timeout](Timeout.md)
* [Editing Reports and Dashboards](Add_Designer.md)
* [Localization](Localization.md)
* [Creating New Reports and New Dashboards](Creating_Report.md)
* [Using Themes](Using_Themes.md)
* [Saving Report and Dashboard](Save_Report.md)
* [Caching](Caching.md)
* [Preview](Preview.md)
* [Events](Events.md)
* [Settings](Settings.md)
