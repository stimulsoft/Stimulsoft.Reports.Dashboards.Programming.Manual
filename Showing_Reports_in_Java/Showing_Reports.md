## Showing Reports

> **Notice**
>
> When a report is assigned to a viewer component, it is automatically generated. You only need to call the `Report.Render()` method if you want to perform specific actions with the rendered report before it is displayed in the viewer. Likewise, when using the compilation mode, you need to call the `Report.Compile()` method only if you have actions to perform with the compiled report before it is built and shown in the viewer.

Add the **StiViewerFx** component on the required component (for example on JFx):


**Jfx**

```
...
StiViewerFx viewerfx = new StiViewerFx(parentFrame);
fx.add(viewerfx);
...
```

where the **JFrameparentFrame** is a main Frame of the application. For better showing **StiViewerFx**, the parent component must have **BoxLayoutManager**. For loading and showing the report use the following method:


**Jfx**

```
...
viewerfx.getStiViewModel().loadDocumentFile(documentFile, showProgress);
...
```

where the argument **documentFile** is a file of **mdc** documents, and the boolean value **showProgress** provides the ability to define whether to show the loading progress of the document (if it is set to true then the process is displayed, if false - it is not displayed.) It is also possible to display a report in the form of a dialog box, you can use the method:


**Jfx**

```
...
StiViewerFx viewerfx = new StiViewerFx(parentFrame);
JDialogviewerPopup = viewerfx.createPopup(parentFrame, modal);
viewerPopup.setVisible(true);
...
```

Where the argument **parentFrame** is a frame from which the dialog is displayed, and the Boolean value **modal** - dialog modality. The method returns **JDialog**, which subsequently can make the necessary manipulations, such as resizing, changing dialog parameters, visibility, etc.
