# Flash Viewer

> **YouTube**
>
> Watch videos [for ASP.NET Flash Viewer](https://www.youtube.com/watch?v=JuIey-Mqqgg&list=PL-72PPAq-3SVkQbSOI3O1RrmPD4rY0OQi&index=1). Subscribe to the [Stimulsoft channel](https://www.youtube.com/user/StimulsoftVideos) to find out about the new video lessons uploaded. Leave your questions and suggestions in the comments to the video.


> **Samples**
>
> See on [GitHub](https://github.com/stimulsoft/Samples-ASP.NET-CSharp) examples for working with the ASP.NET Flash Viewer component. All examples are separate projects, grouped into one solution for Visual Studio.

The **Flash Viewer (StiWebViewerFx)** component is designed to view reports in the web browser. You do not need to install the .NET Framework, ActiveX components or any special plug-ins on the client-side. All that is needed a Web browser with Flash support.


With help of **Flash Viewer**, you can view, print and export reports on any computer with any installed operating system, where there is an Internet connection and a Web browser with Flash support.


**Flash Viewer** is divided into two parts - client and server. The client-side is the graphics wrapper of the viewer, implemented using the Flash technology. The server-side is the report engine that uses the .NET Framework to render reports. Also, the server-side contains modules that perform the functions of receiving requests, processing them, and then transferring the linked data to the client-side. These two parts are assembled into one library and presented as an ASP.NET component.


**Flash Viewer** supports many themes, animated interface, bookmarks, interactive reports, editing of report elements on the page, full screen mode, search panel, and other necessary features for viewing reports. Its distinctive feature is the speed of work and the same appearance of both the viewer itself, and viewed reports on any computer with any installed operating system.


In order to use **Flash Viewer** in a Web-project, the installation of the [Stimulsoft.Reports.Web](https://www.nuget.org/packages/Stimulsoft.Reports.Web) NuGet package is required:

* Select 'Manage NuGet Packages...' menu item in the project's pop-up menu;

* In the 'Browse' tab, type 'Stimulsoft.Reports.Web' in the search textbox;

* Click the Stimulsoft.Report.Web package, select the version of the package and click **Install**. If the package should be updated, use the **Update** button.


If, for some reason, that is not possible, the following assemblies should be added to the project:
* Stimulsoft.Base.dll

* Stimulsoft.Report.dll

* Stimulsoft.Report.Check.dll

* Stimulsoft.Report.Helper.dll

* Stimulsoft.Report.Web.dll

* [How this Work?](How_to_Work.md)
* [Work with Bookmarks](Work_with_Bookmarks.md)
* [Showing Reports](Showing_Reports.md)
* [Interactive Reports](Interaction.md)
* [Connecting Data](Connecting_Data.md)
* [Sending Reports by Email](Send_Email.md)
* [Localization](Localization.md)
* [Calling Designer and Viewer](Call_Designer.md)
* [Printing Reports](Printing_Reports.md)
* [Export and Printing Reports from Code](Export_Report_from_Code.md)
* [Exporting Reports](Export_Setting.md)
* [Viewer Events](Event.md)
* [Work with Parameters](Work_with_Parameters.md)
* [Viewer Settings](Settings.md)
