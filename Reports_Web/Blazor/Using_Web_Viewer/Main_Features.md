# Basic Features

The main options of the **Blazor Viewer** contain the following operations: report display, switching between report pages, zoom changing and report display mode. All specified operations are performed without reloading browser page. You don`t need to setting any special options or events to perform them.


The report viewer has a special event the **OnViewerEvent**, which will be invoked after any action of the viewer. At this event you can find out the type of action, which the viewer is performing at the moment and get all parameters of the viewer, transferred to the server side.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer OnViewerEvent="@OnViewerEvent" />

@code
{
    private void OnViewerEvent(StiReportDataEventArgs args)
    {
        var action = args.Action;
        var report = args.Report;
        var parameters = args.RequestParams;
    }
}
```


> **Information**
>
> The event won't be invoked for events that have their own processors - printing, export, interactive actions on a report etc. These events are described separately in the relevant sections of the documentation.
