# Localization

The Blazor Viewer component supports the localization of its interface. To localize the report viewer interface to the language you need, use the special **L****ocalization** property. You should specify the path to the localization XML file (relative or absolute) as the value of this property (relative or absolute).


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Localization="Localization/en.xml" />
```

When loading the report viewer, the localization file will be loaded automatically.
