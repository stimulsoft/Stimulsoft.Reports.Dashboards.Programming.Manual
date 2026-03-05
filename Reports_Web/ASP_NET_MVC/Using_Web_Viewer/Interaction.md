# Dynamic Sorting, Collapsing, and Drill-Down

The **HTML5 Viewer** component supports dynamic sorting, collapsing, and drill-down of reports. Dynamic sorting provides the ability to change the direction of sorting in a rendered report. To do this, click on the component that has the dynamic sorting enabled. Dynamic sorting is carried out in the following directions - **Ascending** and **Descending**. Each time the component is clicked, the sorting direction is reversed.


Multi-level sorting is allowed in the report. To do this, hold down the **Ctrl** key and sequentially click on the sorted components in the report. To reset sorting, you can click on any sorted component without holding down the **Ctrl** key.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Viewer.Interaction_1.png)

A report with dynamic collapsing is an interactive report in which blocks can collapse/expand their content when you click on the block title. Report elements, which can be collapsed/expanded, are indicated by special icons - **[-]** or **[+]**.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Viewer.Interaction_2.png)

When using drill-down, under the main panel of the viewer, the drill-down panel with tabs for drill-down reports will be displayed. The currently displayed report will be highlighted.


![](../../../images/topics/Reports_Web.ASP_NET_MVC.Using_Web_Viewer.Interaction_3.png)

To work with dynamic sorting, collapsing, and drill-down reports, no additional viewer settings are required. A special interaction action is used to perform any actions before sorting, collapsing, or drill-down. It will be called when interactive action of the viewer.


**Index.cshtml**

```
...
@Html.Stimulsoft().StiMvcViewer("MvcViewer1", 
    new StiMvcViewerOptions() {
        Actions =
        {
            Interaction = "ViewerInteraction"
        }
})
...
```


**HomeController.cs**

```csharp
...
public ActionResult ViewerInteraction()
{
    // Some code before any interaction
    // ...
    
    return StiMvcViewer.InteractionResult();
}
...
```

To get the type of action, you can use the parameters of the viewer. The viewer parameters are represented as an object of the **StiRequestParams** class. They are passed to any server-side by any request and contain all necessary information and states of the client part of the viewer. For each type of interactivity, the viewer has a certain type of action:

* **Sorting** – when using column sorting;

* **DrillDown** – when using drill-down in reports;

* **Collapsing** – when using collapsing report blocks.


**HomeController.cs**

```csharp
...
public ActionResult ViewerInteraction()
{
    StiRequestParams requestParams = StiMvcViewer.GetRequestParams();
    switch (requestParams.Action)
    {
        case StiAction.Sorting:
            break;
        
        case StiAction.DrillDown:
            break;
        
        case StiAction.Collapsing:
            break;
    }
    
    return StiMvcViewer.InteractionResult();
}
...
```
