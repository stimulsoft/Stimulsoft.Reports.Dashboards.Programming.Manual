# Working with Bookmarks

The viewer supports report bookmarks. When such a report is displayed, a panel with bookmarks will appear to the left of the page. When you select a report bookmark, the viewer will automatically navigate to the desired page, and the report element associated with the bookmark will be highlighted.


### Bookmark settings

By default, the width of the bookmarks bar is 180 pixels; the viewer allows you to change this value. The `bookmarksTreeWidth` property is used for this, the value of which is specified in pixels.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.appearance.bookmarksTreeWidth = 300
```

If you do not need to work with report tabs, you can completely disable this functionality. The `showBookmarksButton` property is used for this. It should be set to `False`.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.toolbar.showBookmarksButton = False
```


> **Information**
>
> In this case, report bookmarks will not be shown, even if they are present in the displayed report. This property does not affect printing and exporting a report with bookmarks.

When printing a report with bookmarks, the bookmarks tree will be hidden. If, in addition to the report itself, you also need to print bookmarks, then you need to set the `bookmarksPrint` property to `True`.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.appearance.bookmarksPrint = True
```
