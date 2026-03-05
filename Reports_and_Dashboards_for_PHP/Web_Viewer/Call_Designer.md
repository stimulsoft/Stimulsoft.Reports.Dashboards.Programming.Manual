# Calling Designer from Viewer

The viewer can invoke the report designer. A special button labeled **Design** on the viewer's toolbar is available for this purpose. By default, this button is disabled. To use this feature, you need to set the `showDesignButton` property to `true` and define the `onDesignReport` event:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->options->toolbar->showDesignButton = true;
    $viewer->onDesignReport = 'designReport';
    $viewer->process();
?>

<script>
    function designReport(args) {
        window.open("designer.php?fileName=" + args.fileName);
    }
</script>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Viewer/Showing%20a%20Report%20in%20the%20Viewer%20in%20an%20HTML%20template.php).


A detailed description of available event arguments is in the [Viewer Events](Events.md) section.


> **Information**
>
> The viewer itself doesn’t launch the designer, it simply triggers the event and passes the report and file name as arguments. In the event, you can redirect to a PHP page that hosts the report designer.
