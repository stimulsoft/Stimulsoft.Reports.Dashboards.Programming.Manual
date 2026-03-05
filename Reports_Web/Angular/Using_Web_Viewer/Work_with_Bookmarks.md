# Work with Bookmarks

The **Angular Viewer** component supports report bookmarks. When displaying such a report on the left side of the page, a panel with bookmarks will be displayed. When you select a bookmark of the report, the viewer will carry out an automatic transition to the specified page, and the report item with a bookmark is highlighted.


![](../../../images/topics/Reports_Web.Angular.Using_Web_Viewer.Work_with_Bookmarks_1.png)

By default, the bookmarks bar width is 180 pixels, the **Angular Viewer** component allows you to change this value. For this, the **BookmarksTreeWidth** property, which value is specified in pixels, is used.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Appearance.BookmarksTreeWidth = 200;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```

If work with report bookmarks is not required, you can disable this feature. For this, set the **ShowBookmarksButton** property to **false**.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Toolbar.ShowBookmarksButton = false;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```


> **Information**
>
> In this case, report bookmarks will not be displayed, even if they are present in the displayed report. This property has no effect on printing and exporting reports.

When printing a report with bookmarks, the bookmark tree will be hidden. If you want to print bookmarks with the report, it is necessary to set the **BookmarksPrint** property to **true**.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Appearance.BookmarksPrint = true;
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```
