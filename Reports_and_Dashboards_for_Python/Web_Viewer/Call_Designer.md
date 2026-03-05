# Calling Designer from Viewer

The viewer has the ability to call the report designer (use the **Design** button on the viewer toolbar). By default, this button is disabled. Set the `showDesignButton` property to `True`, and also define the `onDesignReport` event.


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.onDesignReport += 'designReport'
```


**viewer.html**

```html

<script>
    function designReport(args) {
        window.location.href = "/designer?report=" + args.fileName;
    }
</script>
```

A detailed description of the available argument values you may read in the [Viewer Events](Events.md) section.


> **Information**
>
> The viewer itself does not initiate the designer; it solely triggers the specified event and passes the file name and the report being viewed as arguments. Within the event, you can redirect to the web page hosting the report designer and pass the required parameters.
