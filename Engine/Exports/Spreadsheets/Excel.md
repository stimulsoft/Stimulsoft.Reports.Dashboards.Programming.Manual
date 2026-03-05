## Excel

**Microsoft Excel** is a spreadsheet application written and distributed by Microsoft for Microsoft Windows. It allows using calculation, graphing tools, pivot tables and a macro programming language called VBA. So, it is the most popular table processor available for these platforms since version 5 in 1993.


Microsoft Excel up until Excel 2007 version used a proprietary binary file format called Binary Interchange File Format (BIFF) and **.xls** file extension. Specification was closed but since 2008 it was published. Besides, most of Microsoft Excel can read CSV, DBF, SYLK, DIF, and other formats.

### Export Settings

The export parameters of the XLS export are described in the **StiExcelExportSettings** class. The description of all class properties are in the table below.


| ImageQuality | float | image quality; may have values from 0.0 (the lowest quality) to1.0 (the highest quality); by default 0.75 |
| --- | --- | --- |
| ImageResolution | float | image resolution, dot per inch; may have any value, by default 100 |
| UseOnePageHeaderAndFooter | bool | remove from a report all page headers (except the first one) and all page footers (except the last one); by default false |
| ExportDataOnly | bool | export data only, e.g. all components which are placed on data bands; by default false |
| ExportPageBreaks | bool | export page breaks; by default false |
| ExportObjectFormatting | bool | export object formatting; by default true |
| ExportEachPageToSheet | bool | export each page of a report as a sheet; by default false |

The **ExportObjectFormatting** property works only if the ExportDataOnly is set to true.


### Static Options

Static properties of export to Excel. To access to export properties it is necessary to add the **StiOptions.Export.Excel...** prefix. For example, **StiOptions.Export.Excel.AllowExportDateTime**.


| AllowExportDateTime | bool | export date and time; if false then date and time are exported as text strings; by default false |
| --- | --- | --- |
| ColumnsRightToLeft | bool | set the order of columns from right to left; by default false |
| MaximumSheetHeight | int | maximal number of rows on a sheet; remaining rows are transferred on the next sheet; by default 65534 |
| RemoveEmptySpaceAtBottom | bool | remove empty space on the bottom of a page; by default true |
| ShowGridLines | bool | show grid lines; by default true |
| DivideBigCells | bool | divide big cells into smaller ones for easier editing and scrolling; by default true |
