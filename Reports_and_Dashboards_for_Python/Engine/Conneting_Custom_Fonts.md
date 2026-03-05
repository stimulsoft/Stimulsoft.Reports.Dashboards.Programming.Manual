# Connecting Custom Fonts

The report generator provides the ability to load custom fonts from a file or directory. This is done using the static class `StiFontCollection`, which contains the necessary functions for working with fonts.


To connect a font file, use the `addFontFile` function. You need to specify the path to the font file, and optionally, the font name and style. If the font name or style is not specified, the parameters from the font file itself will be used. Example of connecting a font file:


**app.py**

from stimulsoft_reports import StiFontCollectionfrom stimulsoft_reports.enums import FontStyle

StiFontCollection.addFontFile('Roboto.ttf', 'Roboto');

StiFontCollection.addFontFile('Roboto-Black.ttf', 'Roboto Black', FontStyle.BOLD)

Additionally, there is a feature that allows loading all fonts located in a specific directory. To do this, simply specify the required font directory using the `setFontsFolder` function, for example:


**app.py**

from stimulsoft_reports import StiFontCollection
StiFontCollection.setFontsFolder('/fonts')
