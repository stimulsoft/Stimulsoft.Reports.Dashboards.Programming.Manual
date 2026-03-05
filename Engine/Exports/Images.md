# Images

Export groups to graphic formats. All graphic formats can be divided in to types: bitmapped images and vector formats. Notice. On the current moment the export of monochrome image is supported only to the BMP, GIF, PCX, PNG, TIFF

format. So the DitheringType property works only for these exports.

### Export Parameters

All exports of images have the same export settings. They are described in the table below. But each format has its own ExportSettings class. For BMP, GIF, PNG, TIFF, JPEG, PCX, and EMF the following classes are used in exports. The StiBmpExportSettings is used for export to BMP, **StiGifExportSettings** is used for export to GIF, **StiPngExportSettings** is used for export to PNG, **StiTiffExportSettings** is used for export to TIFF, **StiJpegExportSettings** is used for export to JPEG, **StiPcxExportSettings** is used for export to PCX, and **StiEmfExportSettings** is used for export to EMF.


| **Name** | **Type** | **Description** |
| --- | --- | --- |
| ImageZoom | double | zoom factor. By default a value is 1.0 what is equal 100% in export settings window |
| CutEdges | bool | cut page edges; by default false |
| ImageFormat | StiImageFormat | Image format - colored, tint of grey or monochrome; by default StiImageFormat.Color |
| MultipleFiles | bool | saves pages of a report into separate files; can be used for TIFF only, because it can save some pages into one file, other formats save pages into separate files; by default false |
| DitheringType | StiMonochromeDitheringType | a type of image dithering to get monochrome image; by default StiMonochromeDitheringType.FloydSteinberg |
