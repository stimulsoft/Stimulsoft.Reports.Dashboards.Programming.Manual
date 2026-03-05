# Work with Bookmarks

The **HTML5 Viewer** component supports report bookmarks. A panel with bookmarks will be displayed when displaying such a report on the left side of the page. When you select a bookmark of the report, the viewer will carry out an automatic transition to the specified page, and the report item with a bookmark is highlighted.


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Viewer.Work_with_Bookmarks_1.png)

By default, the bookmarks bar width is 180 pixels. The **HTML5 Viewer** component allows you to change this value. For this, the **BookmarksTreeWidth** property, which value is specified in pixels, is used.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    BookmarksTreeWidth="200">
</cc1:StiWebViewer>
...
```

If you do not need to work with report bookmarks, you can disable this option. For this, set the **ShowBookmarksButton** property to **false**.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    ShowBookmarksButton="false">
</cc1:StiWebViewer>
...
```


> **Information**
>
> In this case, report bookmarks will not be displayed, even if they are present in the displayed report. This property does not affect printing and exporting reports.

When printing a report with bookmarks, the bookmark tree will be hidden. If you want to print bookmarks with the report, it is necessary to set the **BookmarksPrint** property to **true**.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    BookmarksPrint="true">
</cc1:StiWebViewer>
...
```
