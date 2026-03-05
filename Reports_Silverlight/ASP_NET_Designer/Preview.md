## Preview

You can preview the report in the window of the Web-designer by selecting the **Preview** tab in the designer. The picture below shows tabs of the Web-designer:


![](../../images/topics/Reports_Silverlight.ASP_NET_Designer.Preview_1.png)


Data are required to preview a rendered report. By default, data specified in the **Dictionary** of the edited report are taken. If it is necessary, they can be overridden. Below is a sample code with which overrides the data:


**C#**

```csharp
...
protected void StiWebDesignerSL1_GetPreviewDataSet(object sender, StiWebDesignerSL.StiPreviewDataSetEventArgs e)
{
    DataSet data = new DataSet();
    data.ReadXml("D:\\Demo.xml");
    data.ReadXmlSchema("D:\\Demo.xsd");
    e.PreviewDataSet = data;
}
...
```

As can be seen from the code, the data is taken from XML and XSD files. In the same way you can substitute the data from other data sources.
