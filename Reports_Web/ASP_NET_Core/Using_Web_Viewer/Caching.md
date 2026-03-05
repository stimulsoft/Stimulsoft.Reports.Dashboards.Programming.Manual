# Caching

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The **HTML5 Viewer** component allows you to use the server cache to store rendered reports. If you do not use caching, you should load the report, connect data, and render it again every time you request a page. If you use caching, the previously rendered report will be loaded from the cache every time you refresh the page.


When using caching, it should be taken into account that every report saved in the cache takes up server memory and, with a large number of requests to reports, this can become a critical issue. Therefore, you need to choose between two options: low memory requirements but high in performance or low-performance requirements but high in memory.


You need to connect modules to work with a session or cache on the server-side to use caching. To do this, just add the following services to the project in the start file of a project.


**Startup.cs**

```csharp
...
public void ConfigureServices(IServiceCollection services)
{
    services.AddMemoryCache();
    services.AddSession();
    services.AddMvc();
}
...
```

You can manage caching with the following properties.


### The CacheMode property

This property of the viewer enables caching and sets its type. It can take one of the following values, specified in the **StiServerCacheMode** enumeration:


**None** – caching is disabled. Each action of the viewer requires loading the report from the file and, if it is a report template, then render it;

**ObjectCache** – for caching, the server cache is used. The report object is saved in this cache (set by default);

**StringCache** – for caching, the server cache is used. The report is saved as a packed string in this cache;

**ObjectSession** – the current session, in which the report object is saved, is used for caching;

**StringSession** – for caching, the current session is used. The report is saved as a packed string in this cache.


### The CacheItemPriority property

This property sets the priority of the report stored in the server's cache. It affects the automatic clearing of the server memory in case of a lack of memory. The lower the priority is, the greater is the chance of removing information from memory.


### The CacheTimeout property

This property specifies the amount of time in minutes for which you want to save the report in the server cache. If you use caching and the requested report is not found in the cache (the objects storage time has expired), then it will be requested again using a special **GetReport** event, then connect the report data and render it.


### StiCacheHelper

The **HTML5 Viewer** component provides the ability to define your methods of working with report caching. For this purpose, a special class **StiCacheHelper** is used. It contains methods for obtaining a report from the cache and saving the report to the cache. It is necessary to create a new class inherited from **StiCacheHelper** and reload the above methods, which respectively have the names - **GetReport**, **SaveReport** and **RemoveReport**.


**HomeController.cs**

```csharp
...
public class ViewerController : Controller
{
    public class StiMyCacheHelper : StiCacheHelper
    {
        public override StiReport GetReport(string guid)
        {
            string path = System.IO.Path.Combine(this.HttpContext.Server.MapPath("CacheFiles"), guid);
            if (System.IO.File.Exists(path))
            {
                StiReport report = new StiReport();
                string packedReport = System.IO.File.ReadAllText(path);
                if (guid.EndsWith("template")) report.LoadPackedReportFromString(packedReport);
                else report.LoadPackedDocumentFromString(packedReport);
                
                return report;
            }
            return null;
            
            //return base.GetReport(guid);
        }
    
        public override void SaveReport(StiReport report, string guid)
        {
            string packedReport = guid.EndsWith("template") ? report.SavePackedReportToString() : report.SavePackedDocumentToString();
            string path = System.IO.Path.Combine(this.HttpContext.Server.MapPath("CacheFiles"), guid);
            System.IO.File.WriteAllText(path, packedReport);
            
            //base.SaveReport(report, guid);
        }
        
        public override void RemoveReport(string guid)
        {
            var path = Path.Combine(HttpContext.Server.MapPath("CacheFiles"), guid);
            if (File.Exists(path))
                File.Delete(path);
        }
    }
    
    static ViewerController()
    {
        StiNetCoreViewer.CacheHelper = new StiMyCacheHelper();
    }
}
...
```

To initialize the work with report caching using the created class, it is enough to set it as a value of the static **StiNetCoreViewer.CacheHelper** property in the controller constructor.


> **Information**
>
> If report caching is disabled (the **CacheMode** property of the viewer is set to **None**), the specified class will not be used.
