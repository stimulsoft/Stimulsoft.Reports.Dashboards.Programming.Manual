## HTML

**HTML** (HyperText Markup Language) is the predominant markup language for Web pages. The majority of web pages are created using the HTML language. The HTML language is interpreted by browser and shown as a document. HTML is a tag language of the document layout. It provides a means to describe the structure of text-based information in a document by denoting certain text as links, headings, paragraphs, lists, etc. Elements are the basic structure for HTML markup. Elements have two basic properties: attributes and content. Each attribute and each element's content has certain restrictions that must be followed for a HTML document to be considered valid. An element usually has a start tag (e.g. <element-name>) and an end tag (e.g. </element-name>).

### Export Settings

The export parameters of the HTML export are described in the **StiHtmlExportSettings** class. The description of all class properties are in the table below.


| Zoom | double | zoom factor. By default a value is 1.0 what is equal 100% in export settings window |
| --- | --- | --- |
| ImageFormat | ImageFormat | sets an image export format; by default ImageFormat.Png |
| ExportMode | StiHtmlExportMode | sets the mode of the document export using the div, span or table elements; by default StiHtmlExportMode.Table |
| ExportQuality | StiHtmlExportQuality | export quality of components size; by default StiHtmlExportQuality.High |
| Encoding | Encoding | file encoding; by default Encoding.UTF8 |
| AddPageBreaks | bool | add page breaks; by default false |
| BookmarksTreeWidth | int | bookmark column width, in pixels; by default 150 |
| ExportBookmarksMode | StiHtmlExportBookmarksMode | a mode the export a document with bookmarks; by default StiHtmlExportBookmarksMode.All |
| UseStylesTable | bool | use the Styles table; if false then the style table is empty and all properties of each component will described directly in the style of this component; by default true |


### Static Options

Except the **StiHtmlExportSettings** class parameters of export to HTML are set using the static properties. All properties are described in the table below. To access to export properties it is necessary to add the **StiOptions.Export.Html...** prefix. For example, **StiOptions.Export.Html.ConvertDigitsToArabic**.


| ConvertDigitsToArabic | bool | convert ASCII digits to Arabic digits; by default false |
| --- | --- | --- |
| ArabicDigitsType | enum | select Arabic digits type; by default Standard |
| AllowImageComparer | bool | use the image comparer, e.g. replace image duplicates (see Common export settings); if false then an image is exported "as is"; by default true |
| ForceWysiwygWordwrap | bool | Forcibly break text in rows as well as in the WYSIWYG mode; by default - false |
| ReplaceSpecialCharacters | bool | change symbols '<', '>', '&', ' " ' on &lt; &gt; &amp; &quot; by default true |
