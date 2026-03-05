## ODT

Open Document Text (**ODT**) is the open document for storing documents of the OpenOffice Writer, which is included into the OpenOffice.org package.


OpenOffice.org is the open package of office applications created as alternative to Microsoft Office. OpenOffice.org was one of the first what supported the new open OpenDocument. Works on Microsoft Windows and UNIX systems: GNU/Linux, Mac OS X, FreeBSD, Solaris, Irix.


OpenDocument Format (ODF) is the open file format for storing office documents, including text documents, spreadsheets, images, data bases, presentations. This format is based on the XML format.


OpenOffice Writer is the text processor and visual HTML editor, included into the OpenOffice. It is open software (LGPL license). Writer is similar to Microsoft Word and has approximately the same functionality. Writer allows saving documents in different formats including Microsoft Word, RTF, XHTML, and OASIS Open Document Format. Starting with the OpenOffice version 2.0, the OpenDocument Format is the default format for saving documents. File have the «.odt» extension.


When exporting the report is converted into a single table. The document is easily editable but some objects can be changed.

### Export Settings

The export parameters of the ODT export are described in the **StiOdtExportSettings** class. The description of all class properties are in the table below.


| ImageQuality | float | image quality; may have values from 0.0 (the lowest quality) to1.0 (the highest quality); by default 0.75 |
| --- | --- | --- |
| ImageResolution | float | image resolution, dot per inch; may have any value, by default 100 |


### Static Options

Static properties of export to ODT. To access to export properties it is necessary to add the **StiOptions.Export.Odt...** prefix. For example, **StiOptions.Export.Odt.DivideSegmentPages**.


| DivideSegmentPages | bool | divide segmented pages into separate pages; if false then are exported "as is" without dividing; by default true |
| --- | --- | --- |
| AllowImageComparer | bool | use the image comparer, e.g. replace image duplicates (see Common export settings); if false then an image is exported "as is"; by default true |
| RemoveEmptySpaceAtBottom | bool | remove empty space on the bottom of a page; by default true |
