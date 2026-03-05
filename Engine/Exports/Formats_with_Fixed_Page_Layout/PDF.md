## PDF

**PDF** (Portable Document Format) – is a file format created by Adobe Systems for document exchange used to create electronic editions using the Adobe Acrobat package. The PDF format is a file text format that is used to publish documents on any platform and OS. The PDF document contains one or more pages. Each page may contain any components: text, graphic and illustrations, information, that provides navigation across the document.


Export to PDF is based on the "Adobe Portable Document Format, Version 1.3, second edition", using some elements of latest format specifications.


> **Information**
>
> Now, when exporting to PDF, the fields for which **Printable=false** are exported to a separate layer that is not printed in Adobe Acrobat. There is one limitation - layers are not supported in the PDF-A compatibility mode, so the **Printable** property is ignored.
>
>
> If you print a report to PDF (**Print to PDF**) from a web viewer, then these fields are not exported.

### Digital Signature

Digital signature is a requisite of an electronic document used to protect this document from falsification. This document is a result of cryptographic conversion of information using the closed key of the electronic signature and allows identifying the owner of the certificate of the key of the signature. Digital signatures are often used to implement electronic signatures


The **StiPdfExportSettings** class is used to control digital signature. It has the following properties:


**C#**

```csharp
...
public bool UseDigitalSignature
public bool UseLocalMachineCertificates
public bool GetCertificateFromCryptoUI
public string SubjectNameString
...
```

By default:


**C#**

```csharp
...
UseDigitalSignature = false;
UseLocalMachineCertificates = true;
GetCertificateFromCryptoUI = true;
SubjectNameString = string.Empty;
...
```

A sample how to use these properties is shown below:


**C#**

```csharp
...
StiReport report = new StiReport();
report.Load("c:\\test.mrt");
report.Render(false);

StiPdfExportSettings settings = new StiPdfExportSettings();
settings.UseDigitalSignature = true;
settings.GetCertificateFromCryptoUI = false;
settings.UseLocalMachineCertificates = true;
settings.SubjectNameString = "John Smith <johns@google.com>";

report.ExportDocument(StiExportFormat.Pdf, "c:\\test.pdf", settings);
...
```

In JavaScript, properties are the same as in C#, and they are located in the class `Stimulsoft.Report.Export.StiPdfExportSettings`. Example of usage:


**JS**

```
...
const report = new StiReport();
report.Load("c:\\test.mrt");

report.renderAsync(function () {
    const settings = new Stimulsoft.Report.Export.StiPdfExportSettings();
    settings.useDigitalSignature = true;
    settings.getCertificateFromCryptoUI = false;
    settings.useLocalMachineCertificates = true;
    settings.subjectNameString = "John Smith <johns@google.com>";
    
    report.exportDocumentAsync(function (data) {
        Stimulsoft.System.StiObject.saveAs(data, "Report.pdf", "application/pdf");
    }, Stimulsoft.Report.StiExportFormat.Pdf, null, settings);
});
...
```


### Encryption

A PDF document can be encoded to protect the content from unauthorized access. A user may set the following parameters of encryption:

User password;

Owner password;

Access permission;

Key length.


Using the StiPdfExportSettings class it is possible to set the encryption parameters from code. The following properties of this class are used:

**C#**

```csharp
...
public string PasswordInputUser
public string PasswordInputOwner
public StiUserAccessPrivileges UserAccessPrivileges
public StiPdfEncryptionKeyLength KeyLength
...
```

The **StiUserAccessPrivileges** enumeration contains the following elements (flags):

None,

PrintDocument,

ModifyContents,

CopyTextAndGraphics,

AddOrModifyTextAnnotations,

All.


The StiPdfEncryptionKeyLength enumeration contains the following elements:

Bit40,

Bit128,

Bit256.


By default the values set as follow:


**C#**

```csharp
...
PasswordInputUser = string.Empty;
PasswordInputOwner = string.Empty;
UserAccessPrivileges = StiUserAccessPrivileges.All;
KeyLength = StiPdfEncryptionKeyLength.Bit40;
...
```

An example of using:


**C#**

```csharp
...
StiReport report = new StiReport();
report.Load("c:\\test.mrt");
report.Render(false);

StiPdfExportSettings settings = new StiPdfExportSettings();
settings.PasswordInputUser = "user";
settings.PasswordInputOwner = "owner";
settings.UserAccessPrivileges = StiUserAccessPrivileges.PrintDocument;
settings.KeyLength = StiPdfEncryptionKeyLength.Bit128;

report.ExportDocument(StiExportFormat.Pdf, "c:\\test.pdf", settings);
...
```

In JavaScript, properties are the same as in C#, and they are located in the class `Stimulsoft.Report.Export.StiPdfExportSettings`. Example of usage:


**JS**

```
...
const report = new StiReport();
report.Load("c:\\test.mrt");

report.renderAsync(function () {
    const settings = new Stimulsoft.Report.Export.StiPdfExportSettings();
    settings.passwordInputUser = "user";
    settings.passwordInputOwner = "owner";
    settings.userAccessPrivileges = StiUserAccessPrivileges.PrintDocument;
    settings.keyLength = StiPdfEncryptionKeyLength.Bit256_r6;

    report.exportDocumentAsync(function (data) {
        Stimulsoft.System.StiObject.saveAs(data, "Report.pdf", "application/pdf");
    }, Stimulsoft.Report.StiExportFormat.Pdf, null, settings);
});
...
```


### Embedded Fonts

By default all embedded fonts are optimized. Characters which are not used in a report are excluded. It allows decreasing the size of a file. But, for correct work of the editable field, the font should be complete. Therefore, for fonts, which are used in editable fields, optimization is not done. This increases the output file size. If Asian languages are used, the file size can be 15-20mb.


If by some reasons the font optimization is not working correct it can be forcibly disabled using the static property:


**C#**

```csharp
...
StiOptions.Export.Pdf.ReduceFontFileSize = false;
...
```


### Editable Fields

To enable the export of editable fields it is necessary to set the static property


**C#**

```csharp
...
StiOptions.Export.Pdf.AllowEditablePdf = true;
...
```

Editable fields in the PDF-file has two conditions:

**First** – a condition before editing, it is shown when opening the file. This condition corresponds to the type of a text box in the preview.

**Second** - the type in the mode of field editing, and after editing. In this condition it is impossible to set the vertical alignment of the text (always Top) and some parameters of a font. Therefore, after editing a field, even if the contents is not changed, the type of this field can be change.


If it is necessary to have the **MultiLine** editable field, then it is necessary to set the **WordWrap** property of the text box to **true**.


### Export Settings

The export parameters of the PDF export are described in the **StiPdfExportSettings** class. The description of all class properties are in the table below.


| **Name** | **Type** | **Description** |
| --- | --- | --- |
| ImageQuality | float | image quality; may have values from 0.0 (the lowest quality) to 1.0 (the highest quality); by default 0.75 |
| ImageResolution | float | image resolution dpi; can take any value, by default 100 |
| EmbeddedFonts | bool | embed font files into the PDF file; is true then all fonts are embedded into the file and this file will have the same look on any computer (there is no need to embed additional fonts); if false then fonts are not embedded; by default true |
| StandardPdfFonts | bool | use standard fonts which are embedded in Adobe Acrobat Reader and there is no need to embed them into the file; all fonts are changed on standard fonts (Courier, Helvetica, Times-Roman); by default false |
| Compressed | bool | compress the PDF file; decreases the file size by compressing the text information (images are always compressed); by default true |
| UseUnicode | bool | writes a text in the Unicode; if false then 190 symbols can be written, and a lot of problems with native language symbols may occur; if true then any symbols can be used; by default true |
| ExportRtfTextAsImage | bool | export RichText objects as images; if false then export tries to convert RichText objects into PDF primitives; if true the RichText is written as an image; by default false |
| PasswordInputUser | string | user password (see Encryption); by default empty string |
| PasswordInputOwner | string | owner password (see Encryption); by default empty string |
| UserAccessPrivileges | enum | user access privileges (see Encryption); by default StiUserAccessPrivileges.All |
| KeyLength | enum | key length (see Encryption);  by default StiPdfEncryptionKeyLength.Bit40 |
| UseDigitalSignature | bool | use digital signature of a document; by default false |
| GetCertificateFromCryptoUI | bool | get the certificate from the Crypto interface; if false then a certificate is searched by certificate identifier without using the interface; by default true |
| SubjectNameString | string | certificate identifier; this is a certificate name (empty string) or a part of a name (substring); by default empty string |
| UseLocalMachineCertificates | bool | search certificates on the local machine; if false then certificate is searched in the store of the current user; by default false |
| CreatorString | string | the "Creator" field in the document description (application name that created the original file); if it is not set (empty string) then the StiOptions.Export.Pdf static property is used. CreatorString; by default empty string |
| KeywordsString | string | the "Keywords" field in the document description (application name that created the original file); if it is not set (empty string) then the StiOptions.Export.Pdf.KeywordsString static property is used; by default empty string |
| ImageCompressionMethod | enum | image compression method - JPEG (with quality loss) or Flate (without quality loss); by default StiPdfImageCompressionMethod.Jpeg |
| DitheringType | enum | using this property as a format of monochrome image (with dithering and without) is defined |

If the **UseUnicode** is used then, for Acrobat Reader 5.0, it is necessary to use the **Embedded fonts = true**. If the **UseUnicode** + encoding is used, then it is necessary to use the **Embedded fonts = true**.


The following should be done to compress file:

enable **Compressed**;

disable **Embedded fonts**;

if Embedded fonts is required then enable the **ReduceFontFileSize**.


### Static Options

Except the **StiPdfExportSettings** class, parameters of export to PDF are also set using the static properties. All properties are described in the table below. To access to export properties it is necessary to add the **StiOptions.Export.Pdf...** prefix.  For example, **StiOptions.Export.Pdf.DivideSegmentPages**.


| DivideSegmentPages | bool | divide segmented pages into separate pages; if false then are exported "as is" without dividing; by default true |
| --- | --- | --- |
| ConvertDigitsToArabic | bool | convert ASCII digits Arabic; by default false |
| ArabicDigitsType | enum | Select Arabic digits type; by default Standard |
| ReduceFontFileSize | bool | optimize embedded fonts - eliminate symbols which are not met in a report; if false then fonts are not changed; by default true |
| AllowEditablePdf | bool | export editable fonts as editable PDF objects (in this case fonts which are used in editable fields are not optimized); if false then editable fields are exported as simple text; by default false |
| AllowImageComparer | bool | use the image comparer, e.g. replace image duplicates (see Common export settings); if false then an image is exported "as is"; by default true |
| AllowImageTransparency | bool | use transparency in export images; by default true |
| AllowInheritedPageResources | bool | store resources of pages in the parent dictionary and inherit from it; if false then resources of pages are specified in each page; this property is critical for some programs of PDF files processing; by default true |
| AllowExtGState | bool | use command to control transparency when creating a document; if false then commands are not used; this property is critical for some programs of PDF files processing; by default true |
| CreatorString | string | the "Creator" field in document description (application name, which created the original document); by default the "Stimulsoft Reports.NET" string |
| KeywordsString | string | the "Keywords" field in document description (keywords); by default empty string |
