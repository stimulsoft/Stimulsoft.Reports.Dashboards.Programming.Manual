# Localization

The **HTML5 Viewer** component supports the complete localization of its interface. To localize the report viewer interface, use the special **Localization** property. The value of this property should specify the path to the localization XML file (relative or absolute).


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1",
    new StiMvcViewerOptions() {
        Localization = "~/Content/Localization/en.xml"
})
...
```

When you load the report viewer, the localization file will be loaded automatically.
