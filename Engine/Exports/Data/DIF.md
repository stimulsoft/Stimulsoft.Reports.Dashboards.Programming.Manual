## DIF

**DIF** (Data Interchange Format) is a text format that is used to exchange sheets between spreadsheets processors  (Microsoft Excel, OpenOffice.org Calc, Gnumeric, StarCalc, Lotus 1-2-3, FileMaker, dBase, Framework, Multiplan, etc). The only limitation of this format is that the DIF format may contain only one sheet in one book.

### Export Settings

The export parameters of the DIF export are described in the **StiDifExportSettings** class. The description of all class properties are in the table below.


| **Name** | **Type** | **Description** |
| --- | --- | --- |
| ExportDataOnly | bool | export data only. e.g. only components placed on data bands; by default false |
| Encoding | Encoding | file encoding; by default Encoding.ASCII |
| UseDefaultSystemEncoding | bool | use the default system encoding; if false then use encoding that is set by the Encoding property; by default true |
