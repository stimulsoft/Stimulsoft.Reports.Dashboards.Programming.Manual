# Work with Bookmarks

The **HTML5 Viewer** component supports report bookmarks. When displaying such a report on the left side of the page, a panel with bookmarks will be displayed. When you select a bookmark of the report, the viewer will carry out an automatic transition to the specified page, and the report item with a bookmark is highlighted.


![](../../images/topics/Reports_JS.Web_Viewer.Work_with_Bookmarks_1.png)

By default, the bookmarks bar width is 180 pixels. The **HTML5 Viewer** component allows you to change this value. The **bookmarksTreeWidth** property, which value is specified in pixels, is used.


**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.appearance.bookmarksTreeWidth = 200;
...
```


If work with report bookmarks is not required, you can disable this functionality. For this, you should set the **showBookmarksButton** property to **false**.

**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.toolbar.showBookmarksButton = true;
...
```


> **Information**
>
> In this case, report bookmarks will not be displayed, even if they are present in the displayed report. This property has no effect on printing and exporting reports.


When printing a report with bookmarks, the bookmark tree will be hidden. If you want to print bookmarks with the report, it is necessary to set the **bookmarksPrint** property to **true**.

**viewer.html**

```html
...
var options = new Stimulsoft.Viewer.StiViewerOptions();
options.appearance.bookmarksPrint = true;
...
```
