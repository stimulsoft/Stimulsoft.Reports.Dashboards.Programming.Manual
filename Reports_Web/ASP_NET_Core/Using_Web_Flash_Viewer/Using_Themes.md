# Using Themes

The **Flash Viewer** component has the ability to change the appearance of visual controls. To change the theme, use the **Theme** property, which can take one of the values of the **StiViewerThemeFx** enumeration.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Theme = StiViewerThemeFx.Office2022
})
...
```

Currently, **4 themes** are available.


![](../../../images/topics/Reports_Web.ASP_NET_Core.Using_Web_Flash_Viewer.Using_Themes_1.png)
