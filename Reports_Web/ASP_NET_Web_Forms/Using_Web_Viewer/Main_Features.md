# Basic Features

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

The main features of the viewer include the following operations - showing reports, switching between report pages, changing the scale, and displaying the preview mode. All specified operations are performed in the AJAX mode without restarting the browser page. No special options or events are required to execute them.


The report viewer has a special **OnViewerEvent** event that will be called when the viewer is running. In this event, you can find out the type of action that the viewer is currently executing and get all viewer parameters passed to the server-side.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnViewerEvent="StiWebViewer1_ViewerEvent">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_ViewerEvent(object sender, StiViewerEventArgs e)
{
    StiAction action = e.Action;
    StiRequestParams parameters = e.RequestParams;
}
...
```
