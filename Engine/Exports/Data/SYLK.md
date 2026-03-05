## SYLK

**SYLK** (Symbolic Link) format- this text format is used to exchange data between applications, specifically spreadsheets. Files of SYLK have «.slk» extension. Microsoft does not publish a SYLK specification, therefore work with this format in different applications can be different.


> **Information**
>
> A SYLK file can be written in Unicode and read by some applications but anyway many applications which do support Unicode writes SYLK files into ANSI but not Unicode. Therefore, symbols which do not have representation in the system code page will be written as ('?') symbols.

### Export Settings

The export parameters of the SYLK export are described in the **StiSylkExportSettings** class. The description of all class properties are in the table below.


| **Name** | **Type** | **Description** |
| --- | --- | --- |
| ExportDataOnly | bool | export data only. e.g. only components placed on data bands; by default false |
| Encoding | Encoding | file encoding; by default Encoding.ASCII |
| UseDefaultSystemEncoding | bool | use the default system encoding; if false then use encoding that is set by the Encoding property; by default true |
