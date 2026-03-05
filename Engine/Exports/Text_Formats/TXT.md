## TXT

**Text file (TXT)** is a kind of computer file that is structured as a sequence of lines. A text file exists within a computer file system. The end of a text file is often denoted by placing one or more special characters, known as an end-of-file marker, after the last line in a text file.


Text files are commonly used for storage of information.

### Export Settings

The export parameters of the TXT export are described in the **StiTxtExportSettings** class. The description of all class properties are in the table below.


| Encoding | Encoding | text file coding; by default Encoding.UTF8 |
| --- | --- | --- |
| DrawBorder | bool | draw border lines; if false, then borders are not drawn; by default true |
| BorderType | StiTxtBorderType | a type of a border line; by default StiTxtBorderType.UnicodeSingle |
| KillSpaceLines | bool | remove all empty rows of a text; by default true |
| KillSpaceGraphLines | bool | remove all rows of a text which contains only blank spaces and symbols of the vertical border; by default true |
| PutFeedPageCode | bool | put feed page code after each page; by default true |
| CutLongLines | bool | cut too long lines of a text which cannot be placed in text boxes; by default true |
| ZoomX | float | horizontal zoom factor by X axis. By default a value is 1.0 what is equal 100% in export settings window |
| ZoomY | float | vertical zoom factor by Y axis. By default a value is 1.0 what is equal 100% in export settings window |


### Static Options

Static properties of export to TXT are shown on the table below. To access to export properties it is necessary to add the **StiOptions.Export.Txt...** prefix. For example, **StiOptions.Export.Txt.ColumnWidths**.


| ColumnWidths | string | forcibly set the text column width (the list through the semicolon); if a row is empty then the column width is not changed; by default empty string |
| --- | --- | --- |
| UseFullTextBoxWidth | bool | use all text box width for a text; in this case if the text is laid on a border, then the border is erased in this place; if false, then when drawing a text, one blank space on the right is always left for correct drawing borders; by default false |
| UseOldMode | bool | use the old mode of the text export; this property is left for keeping compatibility with old versions; by default false |
| UseFullVerticalBorder | bool | draw vertical border outside a cell. So a border will never be closed with a text; by default true |
| UseFullHorizontalBorder | bool | draw horizontal border outside a cell. So a border will never be closed with a text; by default true |
| CheckBoxTextForTrue | string | a text that shows the checkbox true status ; by default "+" |
| CheckBoxTextForFalse | string | a text that shows the check false status; by default "-" |
