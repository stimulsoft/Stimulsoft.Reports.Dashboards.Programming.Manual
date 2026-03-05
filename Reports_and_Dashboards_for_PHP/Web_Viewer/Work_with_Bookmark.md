# Work with Bookmarks

The viewer supports report bookmarks. When such a report is displayed, a bookmarks panel will appear on the left side of the page. By selecting a bookmark, the viewer will automatically navigate to the corresponding page, and the bookmarked report element will be highlighted.


**Bookmarks settings**

By default, the width of the bookmarks panel is set to 180 pixels, but the viewer allows you to change this value using the `bookmarksTreeWidth` property, specified in pixels.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->appearance->bookmarksTreeWidth = 300;
?>
```

If bookmarks aren’t required in the report, this feature can be disabled entirely by setting the `showBookmarksButton` property to `false`.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->showBookmarksButton = false;
?>
```


> **Information**
>
> In this case, report bookmarks will not be displayed, even if they are present in the report. This property doesn’t affect printing or exporting the report.

When printing a report with bookmarks, the bookmarks tree will be hidden. If you need to print both the report and its bookmarks, set the `bookmarksPrint` property to `true`.


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->appearance->bookmarksPrint = true;
?>
```
