## CSV

**CSV** (Comma Separated Values) is a text format that is used to represent table data. Each string of the file is one row of the table. The values of each column are separated by the delimiter that depends on regional settings. The values that contain reserved characters (such as a comma or a new string) are framed with the double quotes ( ") symbol; if double quotes are found in the value they are represented as two double quotes in the file.


> **Information**
>
> Only those data (components) can be exported to the **CSV** format which are placed on data bands. If the **SkipColumnHeaders** property is set to false then, additionally, column headers are exported as the first row.

### Export Settings

The export parameters of the CSV export are described in the StiCsvExportSettings class. The description of all class properties are in the table below.


| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Separator | string | sets the symbol-separator of a list that is used when exporting; by default CurrentCulture.TextInfo.ListSeparator |
| Encoding | Encoding | text file coding; by default Encoding.UTF8 |
| SkipColumnHeaders | bool | skip headers of columns; by default false |


### Static Options

Static properties of export to CSV. To access to export properties it is necessary to add the **StiOptions.Export.Csv...** prefix. For example, **StiOptions.Export.Csv.ForcedSeparator**.


| **Name** | **Type** | **Description** |
| --- | --- | --- |
| ForcedSeparator | string | sets the separator forcibly which are used in export; if the empty string is set then the symbol from export settings in used; by default - empty string |
