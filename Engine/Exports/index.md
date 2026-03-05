## Exports

> **YouTube**
>
> Watch the video tutorials how to [export report](https://www.youtube.com/watch?v=nAgMDJ9Rj-U&index=1&list=PL-72PPAq-3SVXiCXMHVtOHlODCos0wpbA). Subscribe to the [Stimulsoft channel](https://www.youtube.com/user/StimulsoftVideos) and be the first to watch new video lessons. Questions and suggestions is recommended be left in the comments to the video.

This section describes principles of saving rendered reports to different formats, basic characteristics of methods for export, export optimization guidelines data structure which are used in export methods. Stimulsoft Reports supports great many export formats to save rendered reports. Many clients think that there are too many formats. But when you need to get file of definite format type, write only one string of code and the format is not PDF, HTML or RTF, only Stimulsoft Reports may help. We do not think that too many export formats in our report generator is disadvantage and continually work on adding new formats. The more exports the better, as they say.

* [Exports Reports From Code](Export_Reports_From_Code/index.md)
* [Spreadsheets](Spreadsheets/index.md)
* [Formats with Fixed Page layout](Formats_with_Fixed_Page_Layout/index.md)
* [Data](Data/index.md)
* [Web Documents](Web_Documents/index.md)
* [Images](Images.md)
* [Text Formats](Text_Formats/index.md)

### Available File Formats

The **StiExportFormat** enumeration describes export formats. Brief information of exports is represented below.


| **Formats** | **Description** |
| --- | --- |
| **Formats which are used for representing documents and allows for easy viewing and printing** |  |
| [PDF](Formats_with_Fixed_Page_Layout/PDF.md) | export to Adobe PDF. |
| [Microsoft Power Point 2007/2010](Formats_with_Fixed_Page_Layout/Microsoft_Power_Point_2007_2010.md) | export to Microsoft Power Point 2007/2010 |
| [XPS](Formats_with_Fixed_Page_Layout/XPS.md) | export to Microsoft XPS. |
| **Web formats** |  |
| [HTML](Web_Documents/HTML.md) | export to HTML by default. This element duplicates the HTMLTable mode. |
| [HTMLTable](Web_Documents/HTML.md) | export to HTML using the  HTML Table element, to create a report structure. |
| [HTMLSpan](Web_Documents/HTML.md) | export to HTML using the HTML Span element, to create a report structure. |
| [HTMLDiv](Web_Documents/HTML.md) | export to HTML using the HTML Div element, to create a report structure. |
| [MHT](Web_Documents/MHT.md) | export to WebArchive. This format is supported only in Microsoft IE. |
| **Text formats** |  |
| [Text](Text_Formats/TXT.md) | export to Text. |
| [RTF](Text_Formats/RTF.md) | export to Rich Text Format by default. This element duplicates the RTFTable mode. |
| [RTFTable](Text_Formats/RTF.md) | export to Rich Text Format using the RTF Table element, to create a report structure. |
| [RTFFrame](Text_Formats/RTF.md) | export to Rich Text Format using the RTF Frame element, to create a report structure. |
| [RTFWinWord](Text_Formats/RTF.md) | export to Rich Text Format using the Microsoft Word graphic element, to create a report structure. |
| [RTFTabbedText](Text_Formats/RTF.md) | export to Rich Text Format using the symbols of tabulation, to create a report structure. |
| [Word 2007/2010](Text_Formats/Word_2007_2010.md) | export to Microsoft Word 2007/2010. This format is supported starting with Microsoft Office 2007/2010. |
| [ODT](Text_Formats/ODT.md) | export to the OpenDocument Writer file. |
| **Spreadsheets** |  |
| [Excel](Spreadsheets/Excel.md) | export to Microsoft Excel. The file is created using the BIFF (Binary Interchange File Format). |
| [ExcelXML](Spreadsheets/Excel.md) | export to Microsoft Excel XML. The file is created using the XML. This format is supported starting with Microsoft Office 2003. |
| [Excel 2007/2010](Spreadsheets/Excel_2007_2010.md) | export to Microsoft Excel 2007/2010. This format is supported starting with Microsoft Office 2007/2010. |
| [ODS](Spreadsheets/ODS.md) | export to OpenDocument Calc file. |
| **Export as Data** |  |
| [CSV](Data/CSV.md) | export to CSV (Comma Separated Value). |
| [DBF](Data/DBF.md) | export to dBase/FoxPro. |
| [XML](Data/XML.md) | export to XML as data. This format is a saved DataSet. |
| [DIF](Data/DIF.md) | export to DIF (Data Interchange Format). |
| [SYLK](Data/SYLK.md) | export to SYLK (Symbolic Link). |
| **Export as Image** |  |
| [ImageGif](Images.md) | export to GIF. |
| [ImageBmp](Images.md) | export to BMP. |
| [ImagePcx](Images.md) | export to PCX. |
| [ImagePng](Images.md) | export to PNG. |
| [ImageTiff](Images.md) | export to TIFF. |
| [ImageJpeg](Images.md) | export to JPEG. |
| [ImageEmf](Images.md) | export to Windows Metafile. |
