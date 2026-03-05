# HTML5 Viewer

> **YouTube**
>
> Watch videos [.NET Core HTML5 Viewer](https://www.youtube.com/watch?v=SvKzg9viYzc&index=12&list=PL-72PPAq-3SX80j_FIJAcNppiQcOMyGpK). Subscribe to the [Stimulsoft channel](https://www.youtube.com/user/StimulsoftVideos) to find out about the new video lessons uploaded. Leave your questions and suggestions in the comments to the video.


> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-NET.Core-MVC-CSharp) examples for working with the .NET Core HTML5 Viewer component. All examples are separate projects, grouped into one solution for Visual Studio.

The **HTML5 Viewer** (**StiNetCoreViewer**) component is designed for viewing reports in the web browser. You do not need to install the .NET Framework, ActiveX components, or any special plug-ins on the client-side. All that is needed is any modern Web browser.


With the help of **HTML5 Viewer**, you can view, print, and export reports on any computer with any operating system installed. Since the viewer only uses HTML and JavaScript technologies, it can be run on devices with no Flash or Silverlight support - tablets, smartphones. Also, the viewer supports the Touch interface, which is automatically enabled when using devices with a touch screen.


The **HTML5 Viewer** component uses the AJAX technology to perform all actions (uploading a report, paging, scaling, interactivity in reports, etc.), which allows you to get rid of reloading the entire page save Web traffic, and speed up work. The report engine built using the .NET Core technology is used to render reports. This is a cross-platform technology. It allows you to deploy the application on servers that use operating systems like Windows, macOS, and Linux.


The **HTML5 Viewer** supports many themes, animated interface, bookmarks, interactive reports, editing of report elements on the page, full-screen mode, search panel, and other necessary features for viewing reports.


> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

To use the **HTML5 Viewer** in a Web project, you need to install the NuGet package of [Stimulsoft.Reports.Web.NetCore](https://www.nuget.org/packages/Stimulsoft.Reports.Web.NetCore):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Reports.Web.NetCore in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.


To add the ability to view and export dashboards in a Web project, install the NuGet package [Stimulsoft.Dashboards.Web.NetCore](https://www.nuget.org/packages/Stimulsoft.Dashboards.Web.NetCore/) (this package is associated with the package Stimulsoft.Reports.Web.NetCore. If it is missed, it will be installed automatically):

* Select "Manage NuGet Packages ..." in the context menu of the project;

* Specify Stimulsoft.Dashboards.Web.NetCore in the search bar on the Browse tab;

* Select the item, define the version of the package, and click **Install**. When updating the package, click the **Update** button.


* [How this works?](How_to_Work.md)
* [Interactive Reports](Interaction.md)
* [Activation](Activation.md)
* [Timeout](Timeout.md)
* [Showing Reports and Dashboards](Showing_Reports.md)
* [Editing Rendered Reports](Editable.md)
* [Connecting data](Connecting_Data.md)
* [Sending Reports by Email](Send_Email.md)
* [Localization](Localization.md)
* [Calling Designer from Viewer](Call_Designer.md)
* [Printing Reports](Printing_Reports.md)
* [Caching](Caching.md)
* [Exporting Reports and Dashboards](Export.md)
* [Using Themes](Using_Themes.md)
* [Viewing Modes](Mode_of_Show.md)
* [Basic Features](Main_Features.md)
* [Work with Parameters](Work_with_Parameters.md)
* [Additional Methods](Additional_methods.md)
* [Work with Bookmarks](Work_with_Bookmarks.md)
* [Export and Printing from Code](Export_and_Print.md)
* [Viewer Settings](Settings.md)
