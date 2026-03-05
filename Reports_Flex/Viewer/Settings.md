# Settings

It is possible to setup user interface, i.e. it is possible to hide some buttons or panels. On the picture above only 4 buttons of 9 are shown. The code below shows how to get this result:


**Code**

```
...
StiOptions.viewer.toolbar.showOpenButton = false;
StiOptions.viewer.toolbar.showSaveButton = false;
StiOptions.viewer.toolbar.showThumbnailsButton = false;
StiOptions.viewer.toolbar.showBookmarksButton = false;
StiOptions.viewer.toolbar.showFindButton = false;
...
```

In other words each button has the show function. This function has two values: true or false. The default value of this function is true.

### The list of available buttons


* On the toolbar:

* **StiOptions.viewer.toolbar.showPrintButton** - Print button;

* **StiOptions.viewer.toolbar.showOpenButton** - Open button;

* **StiOptions.viewer.toolbar.showSaveButton** - Save button

* **StiOptions.viewer.toolbar.showBookmarksButton** - Bookmark button;

* **StiOptions.viewer.toolbar.showThumbnailsButton** - Thumbnails button;

* **StiOptions.viewer.toolbar.showFindButton** - Find button;

* **StiOptions.viewer.toolbar.showCloseButton** - Close button.


* On the Navigation toolbar:

* **StiOptions.viewer.toolbar.showFirstPageButton** - First Page button;

* **StiOptions.viewer.toolbar.showPreviousPageButton** - Previous Page button;

* **StiOptions.viewer.toolbar.showGoToPageButton** - GoToPage button;

* **StiOptions.viewer.toolbar.showNextPageButton** - Next Page button;

* **StiOptions.viewer.toolbar.showLastPageButton** - Last Page button.


* On the View Page toolbar:

* **StiOptions.viewer.toolbar.showPageViewModeSingleButton** - Single Page button;

* **StiOptions.viewer.toolbar.showPageViewModeContinuousButton** - Continuous Page button;

* **StiOptions.viewer.toolbar.showPageViewModeMultipleButton** - Multiple Page button.

Also it is possible to disable the Zoom panel, see the following:


**Code**

```
...
StiOptions.viewer.toolbar.showZoom = false
...
```
