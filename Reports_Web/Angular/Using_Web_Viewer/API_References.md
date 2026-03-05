# API References

You can using Angular Viewer API. **StiAngularViewer** contains api object that allow to manipulate viewer or view states.


**app.component.ts**

```typescript
...
export class AppComponent {
    @ViewChild('viewer') viewer: StimulsoftViewerComponent;...
}
...
```

Enhance app.component.html, add reference to component, add display current page & zoom, add buttons that allow to zoom page to 50% & export report to PDF format with setting ImageQuality to 200:


**app.component.html**

```html
...
Zoom is {{ viewer.api.zoom }}<br />
Current page {{ viewer.api.currentPage + 1 }}<br />
<input type="button" (click)="viewer.api.zoom = 50" value="Zomm to 50%" />
<input
    type="button"
    (click)="viewer.api.export('Pdf', { ImageResolution: 200 })"
    value="Export to PDF"
/>

<stimulsoft-viewer-angular
    #viewer
    [requestUrl]="'http://localhost:60801/Viewer/{action}'"
    [action]="'InitViewer'"
    [height]="'600px'"
></stimulsoft-viewer-angular>
...
```

### Options

Angular **stimulsoft-viewer-angular** contains options.


| **Parameter** | **Description** |
| --- | --- |
| requestUrl | Url to server instance, must contains placeholder {action} that will replace with action. Example: http://server.url:51528/Viewer/{action} |
| action | Controller action that handle viewer initial request. |
| properties | Properties that will transfer to controller action as JSON object. |
| width | Viewer width. |
| height | Viewer height. |
| backgroundColor | Viewer background color. |
| style | Style of viewer applied to main span as [style]="style". |

### Events

Angular **stimulsoft-viewer-angular** contains events.


| **Parameter** | **Description** |
| --- | --- |
| loaded | Occurs when report loaded. |
| error | Occurs on error, $event is ErrorMessage object contains error: string & type: any  (if present). |
| export | Occurs on export, $event object contains exportFormat: string & exportSettings: {}. |
| email | Occurs on export & email, $event object contains exportFormat: string & exportSettings: {}. |
| print | Occurs on export & email, $event object contains format: string : 'PrintPdf' or 'PrintWithoutPreview' or 'PrintWithPreview'. |

### Methods

With API property of **stimulsoft-viewer-angular** (**StiAngularViewer**) you can perform different actions.


| **Parameter** | **Description** |
| --- | --- |
| currentPage | Get or set the current page number. |
| pageCount | The total pages count. |
| viewMode | Get or set the view mode, can be 'SinglePage', 'Continuous' & 'MultiplePages'. |
| zoom | Get or set the page zoom in percent. From 1 to 1000. |
| zoomPageHeight() | Zoom page in height. |
| zoomPageWidth() | Zoom page in width. |
| printPdf() | Print current report to PDF. |
| printWithoutPreview() | Print current report without preview. |
| printWithPreview() | Print current report/dashboard with preview. |
| showExportForm(format: string) | Show export form. **format** The format to export, can be 'Document', 'Pdf', 'Xps', 'Ppt2007', 'Html', 'Html5', 'Mht', 'Text', 'Rtf', 'Word2007', 'Odt', 'Excel', 'ExcelBinary', 'ExcelXml', 'Excel2007', 'Ods', 'Csv', 'Dbf', 'Dif', 'Sylk', 'Json', 'Xml', 'ImageBmp', 'ImageGif', 'ImageJpeg', 'ImagePcx', 'ImagePng', 'ImageTiff', 'ImageEmf', 'ImageSvg', 'ImageSvgz' |
| showExportEmailForm(format: string) | Show export form & email. **format** The format to export, can be 'Document', 'Pdf', 'Xps', 'Ppt2007', 'Html', 'Html5', 'Mht', 'Text', 'Rtf', 'Word2007', 'Odt', 'Excel', 'ExcelBinary', 'ExcelXml', 'Excel2007', 'Ods', 'Csv', 'Dbf', 'Dif', 'Sylk', 'Json', 'Xml', 'ImageBmp', 'ImageGif', 'ImageJpeg', 'ImagePcx', 'ImagePng', 'ImageTiff', 'ImageEmf', 'ImageSvg', 'ImageSvgz' |
| export(format: string, settings?: any) | Export report to selected format. Use default settings if not specified. **format** The format to export, can be 'Document', 'Pdf', 'Xps', 'Ppt2007', 'Html', 'Html5', 'Mht', 'Text', 'Rtf', 'Word2007', 'Odt', 'Excel', 'ExcelBinary', 'ExcelXml', 'Excel2007', 'Ods', 'Csv', 'Dbf', 'Dif', 'Sylk', 'Json', 'Xml', 'ImageBmp', 'ImageGif', 'ImageJpeg', 'ImagePcx', 'ImagePng', 'ImageTiff', 'ImageEmf', 'ImageSvg', 'ImageSvgz' **settings** The export settings |
| exportEmail(format: string, settings?: any, email?: string, subject?: string, message?: string) | Export report to selected format. Use default settings if not specified. Use default email settings if not specified. **format** The format to export, can be 'Document', 'Pdf', 'Xps', 'Ppt2007', 'Html', 'Html5', 'Mht', 'Text', 'Rtf', 'Word2007', 'Odt', 'Excel', 'ExcelBinary', 'ExcelXml', 'Excel2007', 'Ods', 'Csv', 'Dbf', 'Dif', 'Sylk', 'Json', 'Xml', 'ImageBmp', 'ImageGif', 'ImageJpeg', 'ImagePcx', 'ImagePng', 'ImageTiff', 'ImageEmf', 'ImageSvg', 'ImageSvgz' **settings** The export settings **email** The email **message** The email message **subject** The email subject |
