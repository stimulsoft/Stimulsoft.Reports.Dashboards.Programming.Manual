# Dynamic Sorting, Collapsing, and Drill-Down

In addition to variables that can be set on the parameters panel, the viewer supports other types of interactivity that enhance convenience and functionality when using the report generator. These include sorting, collapsing, and drill-down features.


**Sorting**

Dynamic sorting allows users to change the sorting direction in the generated report. To sort, click on a component where dynamic sorting has been enabled. Sorting can be done in the following directions: **Ascending** and **Descending**. Each time you click on the component, the direction alternates.


Multilevel sorting is also supported. To perform multilevel sorting, hold down the **Ctrl** key and click on the components you want to sort. To reset sorting, click on any sortable component without holding **Ctrl**.


**Collapsing**

A report with dynamic collapsing is interactive, where certain blocks can collapse or expand their content by clicking on the block's header. Collapsible/expandable elements are marked with a special icon, usually a **[-]** or **[+]** sign.


**Drill-Down**

When drill-down is enabled, a drill-down panel with tabs of detailed reports will appear below the main viewer panel. The report currently displayed will be highlighted. Users can close any drill-down pages that are no longer needed.


**Dashboard sorting**

In dashboard viewing mode, many elements allow sorting by data fields either in **Ascending** or **Descending** order.


**Dashboard filtering**

Filtering on a dashboard can be applied through special filtering elements as well as other data components. The filter will affect all interconnected elements on the dashboard.


**Dashboard Drill-Down**

As with reports, dashboards can also have detailed drill-down dashboards or reports. Additionally, for some dashboard elements, data can be drilled down at the element level.


**Viewer interactivity event**

No additional viewer settings are required for dynamic sorting, collapsing, or drill-down actions. However, if you want to execute actions before these interactions, the special event onInteraction is triggered when interactive actions occur in the viewer. A detailed description of available argument values is provided in the [Viewer Events](Events.md) section.


| **Name** | **Desccription** |
| --- | --- |
| `InitVars` | The action occurs during the initialization of report variables requested from the user. |
| `Variables` | The action occurs when using variables on the parameters panel. A detailed description can be found in the [Working with Report Variables](../Engine/Using_Variables.md) section. |
| `Sorting` | The action occurs when using column sorting. |
| `DrillDown` | The action occurs when using column drill-down. |
| `Collapsing` | The action occurs when collapsing report blocks. |
| `DashboardFiltering` | The action occurs when using filters within a dashboard element. |
| `DashboardSorting` | The action occurs when sorting within a dashboard element. |
| `DashboardResetAllFilters` | The action occurs when resetting sorting and filters within a dashboard element to the values defined in the template. |
| `DashboardElementDrillDown` | The action occurs when using drill-down on a dashboard element. |
| `DashboardElementDrillUp` | The action occurs when using drill-down on a dashboard element. |

The corresponding collections of parameters, `sortingParameters`, `collapsingParameters`, and `drillDownParameters`, are passed as arguments, containing data in a specific format necessary for the current interactive action. If needed, the values of the parameter collections can be adjusted while maintaining the structure and order of the transmitted values. Here’s an example of the transmitted parameter values for some interactive actions:


**viewer.php**

```php

<?php
    use Stimulsoft\Viewer\StiViewer;
    
    $viewer = new StiViewer();
    $viewer->onInteraction = 'interaction';
    $viewer->process();
?>

...

<script>
    function interaction(args) {
        switch (args.action) {
            case "Sorting":
                args.sortingParameters = {
                    ComponentName: "Text10;false",
                    DataBand: "DataBand1;DESC;CompanyName"
                };
            break;
    
            case "DrillDown":
                drillDownParameters = [{
                    ComponentIndex: "1"
                    DrillDownMode: null
                    ElementIndex: "6"
                    PageGuid: "b916d048d3f446dc97c356d4ff47f48f"
                    PageIndex: "0"
                    ReportFile: null
                }];
            break;
    
            case "Collapsing":
                args.collapsingParameters = {
                    CollapsingStates: {
                        GroupHeaderBand1: {
                            keys: [1],
                            values: [false]
                        },
                    ComponentName: "GroupHeaderBand1"
                };
            break;
        }
    }
</script>
```

A more detailed description of available argument values is provided in the [Viewer Events](Events.md) section.
