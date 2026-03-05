# Dynamic collapsing, sorting, and detailing

In addition to variables whose values can be set on the parameter panel, the viewer supports other types of interactivity that enhance convenience and functionality when using the report generator. These include sorting, collapsing, and detailing.


### Sorting

Dynamic sorting allows you to change the sorting direction in a built report. To do this, click on the component that has been set up for dynamic sorting. Dynamic sorting is performed in the following directions: **Ascending** and **Descending**. Each click on the component toggles the sorting direction to the opposite.


Multi-level sorting is also supported in the report. To apply it, hold down the **Ctrl** key and click on the sortable components of the report in sequence. To reset the sorting, click on any sortable component without holding the **Ctrl** key.


### Collapsing

A report with dynamic collapsing is an interactive report where specific blocks can collapse or expand their content when clicking on the block's header. Report elements that can be collapsed or expanded are marked with a special icon showing **[-]** or **[+]**.


### Detailing

When drilling down into data, a drill-down panel with tabs for detailed reports will be displayed below the main viewer panel. The currently displayed report will be highlighted. There is an option to close the detailed pages that are not needed at the moment.


### Dashboard Sorting

When viewing a dashboard, many elements allow sorting by the element's data fields in **Ascending** and **Descending** order.


### Dashboard Filtering

Filtering on the dashboard can be done both using special filtering elements and with other elements. The filter will be applied to all related elements on the dashboard.


### Dashboard Drill-Down

In dashboards, as in reports, it is possible to open a drill-down dashboard or report. Additionally, for some dashboard elements, data drill-down at the element level is available.


### Viewer interactivity event

No additional viewer settings are required for any interactive actions in the report or dashboard. However, it’s possible to perform certain operations before an interactive action occurs. To do this, you can define the `onInteraction` event, which will be triggered at the moment an interactive action is performed, just before it is applied to the report. The event arguments will include the action type, the report object, and all parameters used for the current interactive action. Detailed descriptions of the available argument values can be found in the Viewer Events section.


Each type of viewer interactivity has a specific action type listed in the following table:


| **Name** | **Description** |
| --- | --- |
| `InitVars` | The action occurs during the initialization of report variables requested from the user. |
| `Variables` | The action occurs when using variables on the parameters panel. Detailed information can be found in the section [Working with Report Variables](../../Reports_and_Dashboards_for_PHP/Engine/Using_Variables.md). |
| `Sorting` | The action occurs when using column sorting. |
| `DrillDown` | The action occurs when using column detailing. |
| `Collapsing` | The action occurs when collapsing report blocks. |
| `DashboardFiltering` | The action occurs when using filters within a dashboard element. |
| `DashboardSorting` | The action occurs when using sorting within a dashboard element. |
| `DashboardResetAllFilters` | The action occurs when resetting sorting and filters within a dashboard element to the values set in the template. |
| `DashboardElementDrillDown` | The action occurs when using detailing in a dashboard element. |
| `DashboardElementDrillUp` | The action occurs when using detailing in a dashboard element. |

The action type is passed in the event arguments:


**app.py**

```python

from stimulsoft_reports.viewer import StiViewer

viewer = StiViewer()
viewer.onInteraction += 'interaction'
```


**viewer.html**

```html

<script>
    function interaction(args) {
        switch (args.action) {
            case "Sorting":
                break;
            
            case "DrillDown":
                break;
            
            case "Collapsing":
                break;
        }
    }
</script>
```

The arguments include corresponding parameter collections: `sortingParameters`, `collapsingParameters`, `drillDownParameters`, and `filteringParameters`, which contain data in a specific format required for the current interactive action. If needed, the values of the parameter collections can be adjusted while maintaining the structure and order of the passed values. Below is an example of parameter values passed for some interactive actions:


**viewer.html**

```html

<script>
    let sortingParameters = {
        ComponentName: "Text10;false",
        DataBand: "DataBand1;DESC;CompanyName"
    };
 
    let collapsingParameters = {
        CollapsingStates: {
            GroupHeaderBand1: {
                keys: [1],
                values: [false]
            },
            ComponentName: "GroupHeaderBand1"
        };
 
    let drillDownParameters = [{
        ComponentIndex: "1"
        DrillDownMode: null
        ElementIndex: "6"
        PageGuid: "b916d048d3f446dc97c356d4ff47f48f"
        PageIndex: "0"
        ReportFile: null
    }];
</script>
```

Direct access to the parameters of viewer interactive actions on the Python server side isn’t provided, the event only works on the JavaScript client-side.
