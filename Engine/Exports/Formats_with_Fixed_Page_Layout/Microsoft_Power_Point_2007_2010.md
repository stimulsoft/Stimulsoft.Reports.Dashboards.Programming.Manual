## Microsoft Power Point

> **Notice**
>
> For desktop versions, there are no specific size restrictions; the size of the opened file is limited by the free memory of the computer. For web versions, there are limitations: the timeout for download/save operations is set to 1 minute, and usually, files larger than 1 gigabyte cannot be saved.

Microsoft PowerPoint is a presentation program developed by Microsoft. It is a part of the Microsoft Office suite. PowerPoint presentations consist of a number of individual pages or "slides". Slides may contain text, graphics, movies, and other objects, which may be arranged on the slide. The presentation can be printed, displayed on a PC, or navigated through at the command of the presenter. In Stimulsoft Reports each report page corresponds to one slide.

### Export Settings

The export parameters of the PPT export are described in the **StiPpt2007ExportSettings** class. The description of all class properties are in the table below.


| ImageQuality | float | image quality; may have values from 0.0 (the lowest quality) to 1.0 (the highest quality); by default 0.75 |
| --- | --- | --- |
| ImageResolution | float | image resolution dpi; can take any value, by default 100 |


### Static Options

Besides the **StiPpt2007ExportSettings** class, the parameters of the export to PPT are also set using the static properties. All properties are described in the table below. To access to export properties it is necessary to add the **StiOptions.Export.Ppt2007...** prefix. For example, **StiOptions.Export.Ppt2007.ReduceFontFileSize**.


| AllowImageComparer | bool | use the image comparer, e.g. replace image duplicates (see Common export settings); if false then an image is exported "as is"; by default true |
| --- | --- | --- |
| AllowImageComparer | bool | use the image comparer, e.g. replace image duplicates (see Common export settings); if false then an image is exported "as is"; by default true |
