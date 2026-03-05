# Localization

The **Angular Viewer** component supports the complete localization of its interface. To localize the report viewer interface, use the special **Localization** property. The value of this property should specify the path to the localization XML file (relative or absolute).


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Localization = "Localization/en.xml";
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

When you load the report viewer, the localization file will be loaded automatically.
