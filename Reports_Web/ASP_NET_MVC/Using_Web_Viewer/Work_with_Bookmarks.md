# Work with Bookmarks

The **HTML5 Viewer** component supports report bookmarks. A panel with bookmarks will be displayed when displaying such a report on the left side of the page. When you select a bookmark of the report, the viewer will carry out an automatic transition to the specified page, and the report item with a bookmark is highlighted.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Viewer.Work_with_Bookmarks_1.png)

By default, the bookmarks bar width is 180 pixels. The **HTML5 Viewer** component allows you to change this value. For this, the **BookmarksTreeWidth** property, which value is specified in pixels, is used.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Appearance =
        {
            BookmarksTreeWidth = 200
        }
})
...
```

If work with report bookmarks is not required, you can disable this feature. For this, set the **ShowBookmarksButton** property to **false**.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Toolbar =
        {
            ShowBookmarksButton = false
        }
})
...
```


> **Information**
>
> In this case, report bookmarks will not be displayed, even if they are present in the displayed report. This property has no effect on printing and exporting reports.

When printing a report with bookmarks, the bookmark tree will be hidden. If you want to print bookmarks with the report, it is necessary to set the **BookmarksPrint** property to **true**.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Appearance =
        {
            BookmarksPrint = true
        }
})
...
```
