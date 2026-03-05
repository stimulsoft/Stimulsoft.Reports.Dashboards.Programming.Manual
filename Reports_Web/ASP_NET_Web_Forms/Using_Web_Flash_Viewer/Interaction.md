# Dynamic Sorting and Drill-Down

The **Flash Viewer** component supports dynamic sorting, collapsing, and drill-down of reports. Dynamic sorting provides the ability to change the direction of sorting in a rendered report. To do this, click on the component that has the dynamic sorting enabled. Dynamic sorting is carried out in the following directions - **Ascending** and **Descending**. Each time the component is clicked, the direction is reversed.


Multi-level sorting is allowed in the report. To do this, hold down the **Ctrl** key and sequentially click on the sorted components in the report. To reset sorting, you can click on any sorted component without holding down the **Ctrl** key.


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Flash_Viewer.Interaction_1.png)

When using drill-down, under the main panel of the viewer, the drill-down panel with tabs for detailed reports will be displayed. The currently displayed report will be highlighted.


![](../../../images/topics/Reports_Web.ASP_NET_Web_Forms.Using_Web_Flash_Viewer.Interaction_2.png)

To work with dynamic sorting, collapsing and drill-down reports, no additional viewer settings are required. To perform any actions before the sorting, collapsing or drill-down of the report, a special **OnInteraction** event is called, which will be called when interacting with the viewer. For each type of interactivity, the viewer has a certain type of action:

* **Sorting** – when using column sorting;

* **DrillDown** – when using drill-down.


**Default.aspx**

```
...
<cc1:StiWebViewerFx ID="StiWebViewerFx1" runat="server"
    OnInteraction="StiWebViewerFx1_Interaction">
</cc1:StiWebViewerFx>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewerFx1_Interaction(object sender, StiReportDataEventArgs e)
{
    switch (e.Action)
    {
        case StiAction.Sorting:
            break;
        
        case StiAction.DrillDown:
            break;
    }
}
...
```
