# Special Features of PDF/A

PDF/A is an ISO-standardized version of the PDF specialized for use in the archiving and long-term preservation of electronic documents. The PDF/A standard does not define an archiving strategy or the goals of an archiving system. It identifies a "profile" for electronic documents that ensures the documents can be reproduced exactly the same way using various software in years to come. A key element to this reproducibility is the requirement for PDF/A documents to be 100% self-contained. All of the information necessary for displaying the document in the same manner is embedded in the file. This includes, but is not limited to, all content (text, raster images and vector graphics), fonts, and color information. A PDF/A document is not permitted to be reliant on information from external sources.


When the "PDF/A Compliance" mode is enabled, the exported report is subjected to the following restrictions:

- no transparency is allowed (PDF/A-1 only);
- no hyperlinks can be used;
- tooltips are not permitted;
- fonts must always be included;
- document **encryption** is not utilized.

When exporting a report to a PDF document using the PDF/A standard, certain errors may occur. In this chapter, we will discuss some of them.


### The "Font not embedded" error

The PDF-A standard mandates the inclusion of fonts within the PDF file. Consequently, when the "PDF/A Compliance" mode is enabled, the fonts will be automatically included in the PDF export, regardless of the "Embedded fonts" parameter in the export settings. However, in applications utilizing .NET Core and JS components, the report engine can only access fonts that have been loaded into the `StiFontCollection`. Therefore, if a particular font has not been loaded, it will not be incorporated into the resulting PDF file. Consequently, the PDF/A compliance check will display an error indicating that the font has not been embedded.


**HomeController.cs**

```csharp

StiFontCollection.AddFontFile(StiNetCoreHelper.MapPath(this, "Reports/Font.ttf"));
```

### The "Width information for rendered glyphs is inconsistent" error

("Glyph widths in the font dictionary are not consistent with embedded font program widths")

The error message "Width information for rendered glyphs is inconsistent" or "Glyph widths in the font dictionary are not consistent with embedded font program widths" typically occurs when dealing with TrueType or OpenType fonts. These fonts store the contours of symbols as points connected by straight lines or arcs, making them vector fonts. The font file itself contains information about the font, such as:

- Name;
- Coding;
- And a "Widths" table that specifies the width of all the symbols used. This table serves as a cache for viewers, enabling them to quickly process text without calculating the width of characters from the font data each time.


The PDF/A compliance verification process involves multiple stages, one of which is checking the consistency between the data in the Widths table and the actual font data. During this step, the verification utility calculates the width of characters and compares it with the values recorded in the Widths table. According to the standards, a deviation of up to 0.1% is permissible. However, a problem arises due to different graphic libraries calculating character widths differently. As a result, the calculated values may differ, sometimes by 1-2%, which exceeds the allowed deviation of 0.1%. Additionally, different verification utilities may use varying methods to calculate character widths, leading to discrepancies and errors flagged in different files.


> **Notice**
>
> In one instance from our experience, we encountered a scenario where a PDF file underwent verification using Adobe Acrobat Pro successfully, but failed when tested using an online utility. Our graphics library determined the width of a specific character to be 554, a value that was acceptable to Adobe Acrobat. However, upon manually adjusting the number to 553, the file successfully passed the online utility's verification but began to encounter issues with Adobe Acrobat Pro.

While there is no definitive solution to this problem, it is crucial to consider this particular peculiarity when encountering such an error.
