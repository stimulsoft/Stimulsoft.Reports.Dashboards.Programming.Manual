# Appearance

The designer allows for changing the themes of the visual elements. To do this, simply set the `theme` property in the component options:


**designer.php**

```php

<?php
    use Stimulsoft\Designer\StiDesigner;
    use Stimulsoft\Designer\Enums\StiDesignerTheme;
    
    $designer = new StiDesigner();
    $designer->options->appearance->theme = StiDesignerTheme::Office2022BlackGreen;
?>
```

Currently, there are **2 different themes** with their own color accents. As a result, more than **50 design options** are available. This allows customizing the appearance of the designer to match almost any web project design.
