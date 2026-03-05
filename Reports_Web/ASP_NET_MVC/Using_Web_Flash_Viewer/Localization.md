# Localization

The **Flash Viewer** component supports the complete localization of its interface. To localize the report viewer interface, use the special **Localization** property. The value of this property should specify the path to the localization XML file (relative or absolute).


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewerFx("MvcViewerFx1",
    new StiMvcViewerFxOptions() {
        Localization = "~/Content/Localization/en.xml"
})
...
```

If you need to control loading the localization, you need to define a special **GetLocalization** viewer action that will be used to pass the XML localization file to the client-side. As a parameter for the response, you can specify the path to the XML localization file or an XML object that contains the downloaded information from the localization file.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewerFx("MvcViewerFx1",
    new StiMvcViewerFxOptions() {
        Actions =
        {
            GetLocalization = "GetLocalization"
        },
        Localization = "~/Content/Localization/en.xml"
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult GetLocalization()
{
    return StiMvcViewerFx.GetLocalizationResult();
    //return StiMvcViewerFx.GetLocalizationResult(path);
    //return StiMvcViewerFx.GetLocalizationResult(xml);
}
...
```
