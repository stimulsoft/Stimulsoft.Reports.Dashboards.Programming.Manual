## WinForms Viewer

There is a capability to change the mode of showing viewer items and order of showing report pages in WinForms. By default, showing of all elements of the viewer and the display order of pages of the report is left to right. How the viewer will look like can depend on the static **RightToLeft** property of the viewer. If the **RightToLeft** property is set to No, then the viewer items and pages of the report in the viewer window are shown from left to right. Code below show how to set the left to right mode of showing viewer items and report pages:


**C#**

```csharp
...
StiOptions.Viewer.RightToLeft = StiRightToLeftType.No;
...
```

If the **RightToLeft** property is set to **Yes**, then viewer items and report pages in a viewer window are displayed from right to left. The code for setting the right to left mode is shown below:


**C#**

```csharp
...
StiOptions.Viewer.RightToLeft = StiRightToLeftType.No;
...
```
