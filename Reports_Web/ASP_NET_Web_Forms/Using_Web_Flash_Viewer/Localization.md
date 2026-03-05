# Localization

The **Flash Viewer** component supports the complete localization of its interface. To localize the report viewer interface, use the special **Localization** property. The value of this property must specify the path to the localization XML file (relative or absolute).


**Default.aspx**

```
...
<cc1:StiWebViewerFx ID="StiWebViewerFx1" runat="server"
    Localization="Localization/en.xml">
</cc1:StiWebViewerFx>
...
```

When you download the report viewer, the localization file will be loaded automatically.
