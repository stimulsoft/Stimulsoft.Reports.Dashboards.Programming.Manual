## XPS

**XPS** (XML Paper Specification) is the open graphic format of fixed page layout on the base XML (more precisely XAML-based) used to store printed output as electronic documents. This format was developed by Microsoft as alternative to the PDF format.


The XPS document format consists of structured XML markup that defines the layout of a document and the visual appearance of each page, along with rendering rules for distributing, archiving, rendering, processing and printing the documents. The markup language for XPS is a subset of XAML that allows including vector graphic elements, using XAML to mark up the WPF-primitives.


The XPS is a ZIP-archive that contains the files which make up the document. The archive includes page mark up (one file per each page of a document), text, embedded fonts, raster images, 2D vector graphics and other information.

### Export Settings

The export parameters of the XPS export are described in the StiXpsExportSettings class. The description of all class properties are in the table below.


| ImageQuality | float | image quality; may have values from 0.0 (the lowest quality) to 1.0 (the highest quality); by default 0.75 |
| --- | --- | --- |
| ImageResolution | float | image resolution dpi; can take any value, by default 100 |


### Static Options

Besides the **StiXpsExportSettings** class, the parameters of export to XPS are also set using the static properties. All properties are described in the table below. To access to export properties it is necessary to add the **StiOptions.Export.Xps**... prefix. For example, **StiOptions.Export.Xps.ReduceFontFileSize**.


| ReduceFontFileSize | bool | optimize embedded fonts - exclude symbols which are not met in a report; if false then fonts are not changed; by default true |
| --- | --- | --- |
| AllowImageComparer | bool | use the image comparer, e.g. replace image duplicates (see Common export settings); if false then an image is exported "as is"; by default true |
| AllowImageTransparency | bool | use the transparency in exporting images; by default true |
