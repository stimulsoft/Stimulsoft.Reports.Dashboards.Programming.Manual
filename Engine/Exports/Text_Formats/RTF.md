## RTF

Rich Text Format (RTF) is a free document file format developed by Microsoft for cross-platform document interchange. The first version of the RTF standard appeared in 1987. Since that time format specification was changed and added. RTF-documents are supported by many text editors.

### Export Settings

The export parameters of the RTF export are described in the **StiRtfExportSettings** class. The description of all class properties are in the table below.


**Name
              
              
                Type
              
              
                Description

                ImageQuality
              
              
                float
              
              
                image quality; may have values from 0.0 (the lowest quality) to 1.0 (the highest quality); by default 0.75

                ImageResolution
              
              
                float
              
              
                image resolution dpi; can take any value, by default 100

                UsePageHeadersAndFooters
              
              
                bool
              
              
                process headers and footers of a page (see Table mode); by default false

                ExportMode
              
              
                enum
              
              
                select export mode (see Common knowledge); by default StiRtfExportMode.Table

                CodePage
              
              
                int
              
              
                this property is obsolete and is not used any longer, remained for compatibility with earlier versions**


### Static Options

Except the **StiRtfExportSettings** class parameters of export to RTF can be set using the static properties. All properties are described in the table below. To access to export properties it is necessary to add the **StiOptions.Export.Rtf...** prefix. For example, **StiOptions.Export.Rtf.UsePageRefField**.


| UsePageRefField | bool | when exporting a header with page numbers (for example, the "Anchors" report) the MS-Word "PAGEREF" command should be used for page numbers. Page numbers in the table of contents will be dynamically changed; if false, then numbers of pages will be static; by default true |
| --- | --- | --- |
| ConvertDigitsToArabic | bool | convert ASCII digits into Arabic digits; by default false |
| ArabicDigitsType | enum | select type of Arabic digits; by default Standard |
| DivideSegmentPages | bool | divide segmented pages into separate pages; if false then are exported "as is" without dividing; by default true |
| LineHeightExactly | bool | export rows heights of a table "exactly"; if false then the height is exported as "at least"; by default true |
| RemoveEmptySpaceAtBottom | bool | remove empty space on the bottom of a page; by default true |
| LineSpacing | double | coefficient of correction of a row height in multilined text fields; by default 0.965 |
| RightMarginCorrection | int | correction of the right margin of a cell; by default 0 |
| SpaceBetweenCharacters | int | sets space between characters of a font in twips; negative value corresponds to condensation; by default -2 |
| UseCanBreakProperty | bool | use the CanBreak property when exporting rows of a table; by default true |
| DivideBigCells | bool | divide big cells into smaller ones for easier editing and scrolling; by default true |
