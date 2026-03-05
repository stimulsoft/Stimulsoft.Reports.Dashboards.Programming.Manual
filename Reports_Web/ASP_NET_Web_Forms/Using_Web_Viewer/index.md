# HTML5 Viewer

> **YouTube** [for the ASP.NET HTML5 Viewer](https://www.youtube.com/watch?v=JuIey-Mqqgg&list=PL-72PPAq-3SVkQbSOI3O1RrmPD4rY0OQi&index=1)


> **Samples**
>
> See [on GitHub](https://github.com/stimulsoft/Samples-ASP.NET-CSharp) examples for working with the ASP.NET HTML5 Viewer component. All examples are separate projects grouped into one solution for Visual Studio.

The **HTML5 Viewer** (**StiWebViewer**) component is designed for viewing reports in the web browser. You do not need to install the .NET Framework, ActiveX components, or any special plug-ins on the client-side. All you need is any modern Web browser.


With the help of the **HTML5 Viewer**, you can view, print, and export reports on any computer with any operating system installed. Since the viewer only uses HTML and JavaScript technologies, it can be run on devices with no Flash or Silverlight support - tablets, smartphones. Also, the viewer supports Mobile and Touch interfaces, which automatically enable when using mobile devices and touch screen monitors.


The **HTML5 Viewer** component uses the AJAX technology to perform all actions (uploading a report, paging, scaling, interactivity in reports, etc.), allowing you to get rid of reloading the entire page and save Web traffic, and speed up work.


The **HTML5 Viewer** supports many themes, animated interface, bookmarks, interactive reports, editing of report elements on the page, full-screen mode, search panel, and other necessary features for viewing reports.


> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To use the **HTML5 Viewer** in a Web project, you need to install the NuGet package of [Stimulsoft.Reports.Web](https://www.nuget.org/packages/Stimulsoft.Reports.Web):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Reports.Web in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.


If this is not possible, you should add the following assemblies to the project:

* Stimulsoft.Base.dll

* Stimulsoft.Report.dll

* Stimulsoft.Report.Check.dll

* Stimulsoft.Report.Helper.dll

* Stimulsoft.Report.Web.dll


To add the ability to view and export dashboards in a Web project, install the NuGet package [Stimulsoft.Dashboards.Web](https://www.nuget.org/packages/Stimulsoft.Dashboards.Web/) (this package is associated with the package Stimulsoft.Reports.Web. If it is missed, it will be installed automatically):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Dashboards.Web in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.


If for any reason this is not possible, you should additionally add the following assemblies to the project:
* Stimulsoft.Dashboard.dll

* Stimulsoft.Dashboard.Drawing.dll
* Stimulsoft.Dashboard.Export.dll

* [How this Works?](How_to_Work.md)
* [Interactive Reports](Interaction.md)
* [Activation](Activation.md)
* [Timeout](Timeout.md)
* [Showing Reports and Dashboards](Showing_Reports.md)
* [Editing Rendered Report](Editable.md)
* [Connecting Data](Connecting_Data.md)
* [Sending Report by Email](Send_Email.md)
* [Localization](Localization.md)
* [Calling Designer and Viewer](Call_Designer.md)
* [Printing Reports](Printing_Reports.md)
* [Caching](Caching.md)
* [Exporting Reports and Dashboards](Export.md)
* [Export and Printing from Code](Export_and_Print.md)
* [Viewing Modes](Mode_of_Show.md)
* [Basic Features](Main_Features.md)
* [Work with Parameters](Work_with_Parameters.md)
* [Viewer Events](Event.md)
* [Work with Bookmarks](Work_with_Bookmarks.md)
* [Viewer Settings](Settings.md)
