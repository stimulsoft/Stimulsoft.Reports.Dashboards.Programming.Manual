# Caching

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

**HTM5 Designer** uses the server cache to store the editable report template. It is necessary because the client part of the designer contains only a visual representation of components of a report template. The report object itself with all the parameters and properties is stored on the server side.


To use caching, you need to connect modules to work with a session or cache on the server side. To do this, just add the following services to the project in the start file of a project.


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

This property of the designer enables caching and sets its type. It can take one of the following values, specified in the **StiServerCacheMode** enumeration:


**None** – caching is disabled;

**ObjectCache** – for caching, the server cache is used. The report object is saved in this (set by default);

**StringCache** – for caching, the server cache is used. The report is saved as a packed string in this cache;

**ObjectSession** – the current session, in which the report object is saved, is used for caching;

**StringSession** - for caching, the current session is used, in which the report is saved as a packed string.


### The CacheItemPriority property

This property sets the priority of the report stored in the cache of the server. It affects the automatic clearing of the server memory in case of memory shortage. The lower the priority is, the greater is the chance of removing information from memory.


### The CacheTimeout property

This property specifies the amount of time in minutes you want to store the report in the server cache. If, when using caching, the requested report is not found in the cache (time of storing this report expired), then it will be requested again using the special **GetReport** action. In this case the unsaved changes may be lost.


The **HTML5 Designer** component provides the ability to specify its own methods for working with report caching. For this purpose, a special **StiCacheHelper** class is used. It contains methods for obtaining a report from the cache and saving the report to the cache. It is necessary to create a new class inherited from **StiCacheHelper** and reload the above methods which respectively have the names - **GetObject** and **SaveObject**.


**HomeController.cs**

```csharp
...
public class DesignerController : Controller
{
    public class StiMyCacheHelper : StiCacheHelper
    {
        public override object GetObject(string guid)
        {
            string path = System.IO.Path.Combine(this.HttpContext.Server.MapPath("CacheFiles"), guid);
            if (System.IO.File.Exists(path))
            {
                byte[] cacheData = System.IO.File.ReadAllBytes(path);
                return StiCacheHelper.GetObjectFromCacheData(cacheData);
            }
            return null;
            
            //return base.GetObject(guid);
        }
        
        public override void SaveObject(object obj, string guid)
        {
            byte[] cacheData = StiCacheHelper.GetCacheDataFromObject(obj);
            string path = System.IO.Path.Combine(this.HttpContext.Server.MapPath("CacheFiles"), guid);
            System.IO.File.WriteAllBytes(path, cacheData);
            
            //base.SaveObject(obj, guid);
        }
    }

    static DesignerController()
    {
        StiNetCoreDesigner.CacheHelper = new StiMyCacheHelper();
    }
}
...
```

To initialize the work with report caching using the created class, it is enough to set it as the value of the **StiNetCoreDesigner.CacheHelper**  static property in the constructor of the controller.
