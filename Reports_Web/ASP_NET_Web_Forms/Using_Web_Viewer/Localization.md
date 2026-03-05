# Localization

The **HTML5 Viewer** component supports the complete localization of its interface. To localize the report viewer interface, use the special **Localization** property. As a value of this property, you should specify the path to the localization XML file (relative or absolute).


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    Localization="Localization/en.xml">
</cc1:StiWebViewer>
...
```

When you load the report viewer, the localization file will be loaded automatically.
