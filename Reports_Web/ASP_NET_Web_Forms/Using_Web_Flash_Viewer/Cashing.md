# Caching

The **Flash Viewer** component allows you to use the server cache to store rendered reports. If you do not use caching, then, when you print and export the report, the viewer will send the report to the server-side, consuming Internet traffic and slowing down the process of printing and exporting the report. If you use caching, then, with the specified actions, the previously rendered report will be loaded from the cache.


When using caching, it should be taken into account that every report saved in the cache takes up server memory and, with a large number of requests to reports, this can become a critical issue. Therefore, you need to choose from two options - either low memory requirements but high in performance and the volume of transmitted data or low performance requirements and internet traffic but high in memory on the server-side.


You can manage caching with the following properties.


### The CacheMode property

This property of the viewer enables caching and sets its type. It can take one of the following values, specified in the **StiServerCacheMode** enumeration:


**None** – сaching is disabled, when printing and exporting, the report will be sent each time to the server-side;

**ObjectCache** – for caching, the server cache is used. The report object is saved in it (set by default);

**StringCache** - the current session, in which the report object is saved, is used for caching;

**ObjectSession** - for caching, the server cache is used, in which the report is saved as a packed string;

**StringSession** - for caching, the current session is used, in which the report is saved as a packed string.


### The CacheItemPriority property

This property sets the priority of the report stored in the server's cache. It affects the automatic clearing of the server memory in case of memory shortage. The lower the priority is, the greater is the chance of removing information from memory.


### The CacheTimeout property

This property specifies the amount of time in minutes for which you want to save the report in the server cache. If you use caching and the requested report is not found in the cache (the objects storage time has expired), then it will be requested again using a special **OnGetReport** event, then connect the report data and render it.


### StiCacheHelper

The **Flash Viewer** component provides the ability to define your own methods of working with report caching. For this purpose, a special class **StiCacheHelper** is used. It contains methods for obtaining a report from the cache and saving the report to the cache. It is necessary to create a new class inherited from **StiCacheHelper** and reload the above methods, which respectively have the names - **GetReport** and **SaveReport**.


**Default.aspx.cs**

```csharp
...
public partial class _Default : Page
{
    public class StiMyCacheHelper : StiCacheHelper
    {
        public override StiReport GetReport(string guid)
        {
            string path = Path.Combine(HttpContext.Current.Server.MapPath(string.Empty), "CacheFiles", guid);
            if (File.Exists(path))
            {
                StiReport report = new StiReport();
                string packedReport = File.ReadAllText(path);
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
            string path = Path.Combine(HttpContext.Current.Server.MapPath(string.Empty), "CacheFiles", guid);
            File.WriteAllText(path, packedReport);
            
            //base.SaveReport(report, guid);
        }
    }

    static _Default()
    {
        StiWebViewerFx.CacheHelper = new StiMyCacheHelper();
    }
}
...
```

To initialize the work with report caching using the created class, it is enough to set it as a value of the static **StiWebViewerFx.CacheHelper** property in the ASPX page constructor.


> **Information**
>
> If report caching is disabled (the **CacheMode** property of the viewer is set to **None**), the specified class will not be used.
