## ODS

Open Document Spreadsheet (**ODS**) is the opened format to store OpenOffice Calc spreadsheet documents, that is included into the OpenOffice.org package.


OpenOffice.org is a free package of office applications developed as alternative to Microsoft Office. The OpenDocument is one of the first what started to support the opened format. it works on Microsoft Windows and UNIX-like systems: GNU/Linux, Mac OS X, FreeBSD, Solaris, Irix.


OpenDocument Format (ODF) — an open document file format for storing and exchanging editable documents including text documents (such as notes, reports, and books), spreadsheets, drawings, databases, presentations. The format is based on the XML-format. The standard was jointly developed by public and various organizations and is available to all and can be used without restrictions.


OpenOffice Calc is the table processor that is included into the OpenOffice and is a free software (LGPL license). Calc is similar to the Microsoft Excel spreadsheet and functionality of these processors is approximately equal. Calc allows you to saving documents to various formats, including Microsoft Excel, CSV, HTML, SXC, DBF, DIF, UOF, SLK, SDC. Starting with version OpenOffice 2.0, for document storage format by default OpenDocument Format, files are saved with the extension «. Ods». Starting with the OpenOffice version 2.0 for storing documents, by default, the OpenDocument Format is used. Files are stored with the «.ods» extension.

### Export Settings

The export parameters of the ODS export are described in the **StiOdsExportSettings** class. The description of all class properties are in the table below.


| ImageQuality | float | image quality; may have values from 0.0 (the lowest quality) to1.0 (the highest quality); by default 0.75 |
| --- | --- | --- |
| ImageResolution | float | image resolution, dot per inch; may have any value, by default 100 |


### Static Options

Static properties of export to ODS. To access to export properties it is necessary to add the **StiOptions.Export.Ods...** prefix. For example, **StiOptions.Export.Ods.AllowImageComparer**.


| AllowImageComparer | bool | use the image comparer, e.g. replace image duplicates (see Common export settings); if false then an image is exported "as is"; by default true |
| --- | --- | --- |
| DivideSegmentPages | bool | divide segmented pages into separate pages; if false then are exported "as is" without dividing; by default true |
| RemoveEmptySpaceAtBottom | bool | remove empty space on the bottom of a page; by default true |
