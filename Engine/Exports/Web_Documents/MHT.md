## MHT

**MHTML** (MIME HTML) is a web page archive format used to bind resources which are typically represented by external links (such as images, Flash animations, Java applets, audio files) together with HTML code into a single file. This file is a web archive and has the «.mht» extension. The content of a file is written as an Email message using the MIME standard: in the beginning of a file the HTML file is written. Then all resources in the base64 encoding with headers are written. Internet Explorer, Opera, Microsoft Word can work with the MHTML format.

### Export Settings

The export parameters of the MHT export are described in the **StiMhtExportSettings** class. The description of all class properties are in the table below.


**Name
              
              
                Type
              
              
                Description

                Zoom
              
              
                double
              
              
                zoom factor. By default a value is 1.0 what is equal 100% in export settings window

                ImageFormat
              
              
                ImageFormat
              
              
                sets an image export format; by default ImageFormat.Png

                ExportMode
              
              
                StiHtmlExportMode
              
              
                sets the mode of the document export using the div, span or table elements; by default StiHtmlExportMode.Table

                ExportQuality
              
              
                StiHtmlExportQuality
              
              
                export quality of components size; by default StiHtmlExportQuality.High

                Encoding
              
              
                Encoding
              
              
                file encoding; by default Encoding.UTF8

                AddPageBreaks
              
              
                bool
              
              
                add page breaks; by default false

                BookmarksTreeWidth
              
              
                int
              
              
                bookmark column width, in pixels; by default 150

                ExportBookmarksMode
              
              
                StiHtmlExportBookmarksMode
              
              
                a mode the export a document with bookmarks; by default StiHtmlExportBookmarksMode.All**
