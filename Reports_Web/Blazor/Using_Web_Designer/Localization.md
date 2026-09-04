# Localization

> **Information**
>
> The `StiLocalization` class is also available for working with localization. A detailed description of its properties and methods can be found in the  chapter. "[Report Engine - Working with Localization](../../../Engine/Working_with_Localization.md)" chapter.

The **Blazor Designer** component supports the full localization of its interface. The **Localization** property is used to localize the interface of the report designer. You should specify the path to the XML localization file (relative or absolute).


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorDesigner Localization="Localization/en.xml" />
```
