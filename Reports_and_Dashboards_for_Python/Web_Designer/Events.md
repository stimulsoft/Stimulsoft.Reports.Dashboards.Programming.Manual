# Designer Events

The report designer supports events that provide the ability to perform necessary operations before specific actions-both on the JavaScript client side and the Python server side. A detailed description of how events work can be found in the [Report Engine Events](../Engine/Events.md) section.

Some event arguments take values from enumerations that are located in specific namespaces. All the enumerations used in designer events are listed in the code block below:


**app.py**

```python

from stimulsoft_reports.enums import StiEventType
```

The designer supports the following events:

- [onPrepareVariables](#onpreparevariables)
- [onBeginProcessData](#onbeginprocessdata)
- [onEndProcessData](#onendprocessdata)
- [onCreateReport](#oncreatereport)
- [onOpenReport](#onopenreport)
- [onOpenedReport](#onopenedreport)
- [onSaveReport](#onsavereport)
- [onSaveAsReport](#onsaveasreport)
- [onPreviewReport](#onpreviewreport)
- [onCloseReport](#onclosereport)
- [onExit](#onexit)


### onPrepareVariables

[v] JavaScript  [v] Python


The event is triggered before the report is built, after the report variables are prepared. A list of event arguments can be found in the [Report Engine Events](../Engine/Events.md) section. Detailed descriptions and usage examples can be found in the [Working with Report Variables](../Engine/Using_Variables.md) section.

### onBeginProcessData

[v] JavaScript  [v] Python


The event is triggered before requesting the data needed to build the report. A list of event arguments can be found in the [Report Engine Events](../Engine/Events.md) section. Detailed descriptions and usage examples can be found in the [Connecting Data Files](../Engine/Connecting_Data_Files.md) and [Connecting SQL Data Adapters](../Engine/Connecting_SQL_Data.md) sections.

### onEndProcessData

[v] JavaScript  [v] Python


The event is triggered after the data is loaded, before the report is built. A list of event arguments can be found in the [Report Engine Events](../Engine/Events.md) section. Detailed descriptions and usage examples can be found in the [Connecting Data Files](../Engine/Connecting_Data_Files.md) and [Connecting SQL Data Adapters](../Engine/Connecting_SQL_Data.md) sections.

### onCreateReport

[v] JavaScript  [v] Python


The event is triggered after a new report is created in the designer. The table below presents a list of event handler arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event has the value  "`CreateReport`". |
| `sender` | The identifier of the component that initiated this event can take the following value: - "`Designer`" |
| `report` | The current report object. |
| `isWizardUsed` | This flag indicates whether the new report is being created using a wizard (`true`) or as a blank report (`false`). |
| `preventDefault` | This flag provides the ability to stop further event processing. By default, it is set to `false`. |

List of properties passed in the event arguments on the Python server-side. The arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, for this event, it has the value `StiEventType.CREATE_REPORT`. |
| `sender` | The identifier of the component that initiated the event, which can have the following value: - `StiDesigner` |
| `report` | The current report object. |
| `isWizardUsed` | The flag indicates whether the new report is being created using a wizard (`true`), or as a blank report (`false`). |

### onOpenReport

[v] JavaScript  [x] Python


List of properties passed in the event arguments on the JavaScript client-side:


| **Name** | **Desccription** |
| --- | --- |
| `event` | The identifier of the current event, with the value "`OpenReport`". |
| `sender` | The identifier of the component that initiated the event, which can have the following value: - "Designer" |
| `preventDefault` | This flag allows you to stop further event processing by the designer. By default, it is set to `true`. |

### onOpenedReport

[v] JavaScript  [v] Python


The event is triggered after opening a report from the designer menu but before it is loaded into the designer.


List of properties passed in the event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, with the value "`OpenReport`". |
| `sender` | The identifier of the component that initiated the event, which can have the following value: - "`Designer`" |
| `report` | The current report object. |
| `preventDefault` | This flag allows you to stop further event processing by the designer. By default, it is set to `true`. |

List of properties passed in the event arguments on the Python server-side. Arguments have the type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, for this event the value is `StiEventType.OPENED_REPORT`. |
| `sender` | The identifier of the component that initiated the event, which can take the following value: - `StiDesigner` |
| `report` | The current report object. |

### onSaveReport

[v] JavaScript  [v] Python


The event is triggered when saving a report in the designer. Below is the list of arguments passed to the event handler on the JavaScript client side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, with the value "`SaveReport`". |
| `sender` | The identifier of the component that initiated the event, which can take the following value: - "`Designer`" |
| `report` | The current report object. |
| `fileName` | The report file name to save. |
| `autoSave` | This flag indicates whether the report is being saved automatically (`true`), or by clicking the save button (`false`). |
| `preventDefault` | This flag allows stopping further event processing by the designer. By default, it is set to `false`. |

List of properties passed in the event arguments on the Python server-side. Arguments have the type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, for this event the value is `StiEventType.SAVE_REPORT`. |
| `sender` | The identifier of the component that initiated the event, which can take the following value: - `StiDesigner` |
| `report` | The current report, represented as an object. The current report, represented as an object. |
| `fileName` | The report file name to save. |
| `autoSave` | This flag indicates whether the report is being saved automatically (`true`), or manually (`false`). |

### onSaveAsReport

[v] JavaScript  [v] Python


The event is triggered when saving a report in the designer with a pre-entered file name. The list of properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value "`SaveAsReport`". |
| `sender` | The identifier of the component that initiated this event, can have the following values: - `"Designer"` |
| `report` | The current report object. |
| `fileName` | The report file name to save. |
| `preventDefault` | This flag allows stopping further event processing by the designer. By default, it is set to `false`. |

List of properties passed in the event arguments on the Python server side. The arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, for this event, it has the value `StiEventType.SAVE_AS_REPORT`. |
| `sender` | The identifier of the component that initiated this event, can have the following values: - `StiDesigner` |
| `report` | The current report object. |
| `fileName` | The name of the report file to save. |

### onPreviewReport

[v] JavaScript  [v] Python


The event is triggered when switching to the report preview tab.


List of properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value "`PreviewReport`". |
| `sender` | The identifier of the component that initiated this event, can have the following values: - `"Designer"` |
| `report` | The current report object. |
| `viewer` | The current embedded viewer component in the designer. |
| `preventDefault` | This flag allows stopping further event processing by the designer. By default, it is set to `true`. |

List of properties passed in the event arguments on the Python server-side.  The arguments are of type `StiReportEventArgs`:


| **Name** | **Descrription** |
| --- | --- |
| `event` | The identifier of the current event, for this event, it has the value `StiEventType.PREVIEW_REPORT`. |
| `sender` | The identifier of the component that initiated this event, can have the following values: - `StiDesigner` |
| `report` | The current report object. |

### onCloseReport

[v] JavaScript  [v] Python


The event is triggered after the report is closed from the designer menu and before the report has been unassigned from the report designer.


List of properties passed in the event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, with the value "`CloseReport`". |
| `sender` | The identifier of the component that initiated the event, which can have the following value: - "`Designer`" |
| `report` | The current report object. |
| `preventDefault` | This flag allows you to stop further event processing by the designer. By default, it is set to `true`. |

List of properties passed in the event arguments on the Python server-side. Arguments have the type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, for this event the value is `StiEventType.CLOSE_REPORT`. |
| `sender` | The identifier of the component that initiated the event, which can take the following value: - `StiDesigner` |
| `report` | The current report object. |

### onExit

[v] JavaScript  [x] Python


The event is triggered when the **Exit** button is clicked in the main menu of the designer.


List of properties passed in the event arguments on the client-side JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, has the value "`Exit`". |
| `sender` | The identifier of the component that initiated this event, can have the following values: - `"Designer"` |
