# Printing Report

The **Flash Viewer** component provides several options for printing a report. Each has its own advantages and disadvantages.


### Default

The report will be printed directly from the Flash application using built-in printing methods. One of the advantages is the complete similarity of the report preview and printed report, since a graphical snapshot of the report page is sent to the printer. The disadvantages include the large amount of information sent to the printer. Also, small text may look a little blurry. This happens because printing in Flash is done by converting the report page into an image.


### Print as PDF

Printing will be done by exporting the report to the **PDF format**. The advantages are greater accuracy of positioning and printing of the report elements in comparison with other printing options. Among the drawbacks, one can mention the mandatory presence of a plug-in installed in a web browser for viewing PDF files (modern browsers have embedded PDF viewer and printer).


### Print as HTML

The report will be printed by exporting the report to the **HTML format**. Advantages - cross-browser compatibility when printing, no need to install special plug-ins. The disadvantage is the relatively low accuracy of the position of the report elements, due to the peculiarities of the implementation of HTML formatting.


> **Information**
>
> When printing to the **HTML format**, you should check the compliance of report page settings and printer parameters (paper size, orientation, margins, indents), as well as check your browser print settings, such as margins, headers, footers, watermarks printing, color printing.


![](../../../images/topics/Reports_Web.ASP_NET_Core.Using_Web_Flash_Viewer.Printing_Report_1.png)

### Report printing settings

If you choose to print a report on the panel of the viewer, a print dialog with a selection of pages and a print type is displayed. The component **Flash Viewer** has the ability to hide unnecessary printing modes. For this it is enough to set the value to **false** for the corresponding properties of the viewer.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Print =
    {
        AllowDefaultPrint = false,
        AllowPrintToHtml = false,
        AllowPrintToPdf = true
    }
})
...
```

The **Flash Viewer** component can disable the embedded report printing dialog. By clicking on the button, the system print dialog will be displayed immediately, the report will be printed in the **Default** mode. To do this, set the **ShowPrintDialog** property to **false**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Print =
    {
        ShowPrintDialog = false
    }
})
...
```

Also, the **Flash Viewer** component has the ability to completely disable report printing. To do this, set the value of the **ShowPrintButton** property to **false**.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Toolbar =
    {
        ShowPrintButton = false
    }
})
...
```

When printing in **Default** mode, the **Flash Viewer** component allows you to configure advanced print settings. For this purpose, several properties are shown below.


**Index.cshtml**

```
...
@Html.StiNetCoreViewerFx(new StiNetCoreViewerFxOptions() {
    Print =
    {
        AutoPageOrientation = true,
        AutoPageScale = true,
        PrintAsBitmap = true
    }
})
...
```

The **AutoPageOrientation** property enables the automatic report page rotation, if the page orientation does not match the page orientation settings of the printer. By default, the property is set to **true**.


The **AutoPageScale** property enables the report page zoom to be automatically adjusted to the paper size. This allows you to get rid of unnecessary fields and indentation, but it can lead to violation of proportions of some components of the report. This mode is suitable for most common reports. By default, the property is set to **true**.


The **PrintAsBitmap** property enables the report printing mode by means of a snapshot of the report page. When the mode is enabled, the report will be printed as is, as accurately as possible, with all styles and images. If the property is set to **false**, the vector print mode will be enabled, but due to the printing feature in Flash, only text and some graphical elements of the report in black and white mode will be printed. By default, the property is set to **true**.
