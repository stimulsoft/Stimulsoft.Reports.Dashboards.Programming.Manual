# Connecting Custom Fonts

The report generator allows you to load custom fonts from a file or a directory. This is achieved using the static class `StiFontCollection`, which provides the necessary functions for working with fonts.


To connect a font file, use the `addFontFile` function. You need to specify the path to the font file and, optionally, the font name and style. If the font name or style is not specified, the parameters from the font file will be used. Here’s an example of connecting a font file:


**report.php**


<?php

use Stimulsoft\Enums\FontStyle;

use Stimulsoft\StiFontCollection;

StiFontCollection::addFontFile('Roboto-Black.ttf', 'Roboto', FontStyle::Bold);
?>

Additionally, you can load all fonts from a single directory. To do this, specify the directory containing the fonts using the `setFontsFolder` function. For example:


**report.php**


<?php

use Stimulsoft\StiFontCollection;

StiFontCollection::setFontsFolder('/fonts');
?>
