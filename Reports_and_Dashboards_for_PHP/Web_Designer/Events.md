# Designer Events

The report viewer supports events that allow executing necessary operations before certain actions, both on the client JavaScript side and the server PHP side. Detailed descriptions of event handling can be found in the [Report Engine Events](../Engine/Events.md) section.


The viewer supports the following events:

- [onDatabaseConnect](#ondatabaseconnect)

- [onBeginProcessData](#onbeginprocessdata)
- [onEndProcessData](#onendprocessdata)
- [onPrepareVariables](#onpreparevariables)
- [onCreateReport](#oncreatereport)
- [onOpenReport](#onopenreport)
- [onOpenedReport](#onopenedreport)
- [onSaveReport](#onsavereport)
- [onSaveAsReport](#onsaveasreport)
- [onPreviewReport](#onpreviewreport)
- [onCloseReport](#onclosereport)
- [onExit](#onexit)

### onDatabaseConnect

[-] JavaScript  [+] PHP


This event is triggered before connecting to the database after receiving all the parameters. Detailed descriptions and usage examples can be found in the [Connetting SQL Data Adapter](../Engine/Connecting_SQL_Data.md) section. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.

### onBeginProcessData

[+] JavaScript  [+] PHP


This event is triggered before requesting the data needed to generate the report. Detailed descriptions and usage examples can be found in the [Connecting Data](../Engine/Connecting_Data_Files.md) and[Connetting SQL Data Adapter](../Engine/Connecting_SQL_Data.md) sections. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.


### onEndProcessData

[+] JavaScript  [+] PHP


This event is triggered before requesting the data needed to generate the report. Detailed descriptions and usage examples can be found in the [Connecting Data](../Engine/Connecting_Data_Files.md) and[Connetting SQL Data Adapter](../Engine/Connecting_SQL_Data.md) sections. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.


### onPrepareVariables

[+] JavaScript  [+] PHP


This event is triggered before generating the report, after preparing the report variables. Detailed descriptions and usage examples can be found in the [Working with Report Variables](../Engine/Using_Variables.md) section. A list of event arguments is available in the [Report Engine Events](../Engine/Events.md) section.

### onCreateReport

[+] JavaScript  [+] PHP


The event is triggered after a new report is created in the designer. Detailed descriptions and usage examples can be found in the [Creating and Editing a Report](Creating_Editing_Report.md) section.


The table below lists the properties passed in the event arguments on the client-side using JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, which has the value  "`CreateReport`". |
| `sender` | The identifier of the component that triggered this event, which can have the following values: - `"Designer"` |
| `report` | The current report object. |
| `isWizardUsed` | A flag indicating whether the new report is created using a wizard (value `true`) or as a blank report (value `false`). |

The table below lists the properties passed in the event arguments on the server-side using PHP. The arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, which for this event has the value `StiEventType::CreateReport`. |
| `sender` | The component that triggered this event, which can have the following types: - `StiDesigner` |
| `report` | The current report object. |
| `isWizardUsed` | A flag indicating whether the new report is created using a wizard (value `true`) or as a blank report (value `false`). |

### onOpenReport

[+] JavaScript  [-] PHP


This event is triggered after opening a report after clicking the toolbar button.
The table below contains a list of properties passed as event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`OpenReport`". |
| `sender` | The identifier of the component that triggered this event can have the following values: - `"Designer"` |
| `preventDefault` | This flag allows you to stop further processing of the event by the viewer. The default value is `true`. |

**onOpenedReport**

[+] JavaScript  [+] PHP


The event is triggered after the report is opened from the designer menu and before it is passed to the designer itself.
The table below lists the properties passed in the event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value `"OpenedReport"`. |
| `sender` | The identifier of the component that triggered this event can have the following values: - `"Designer"` |
| `report` | The current report object. |
| `preventDefault` | This flag allows you to stop further processing of the event by the viewer. The default value is `true`. |

The table below lists the properties passed in the event arguments on the PHP server-side, the arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, which for this event has the value `StiEventType::OpenedReport` |
| `sender` | The component that triggered this event, which can have the following types: - `StiDesigner` |
| `report` | The current report object. |

### onSaveReport

[+] JavaScript  [+] PHP


The event is triggered when saving a report in the designer. Detailed descriptions and usage examples can be found in the [Saving a Report](Saving_Report.md) section.


The table below lists the properties passed in the event arguments on the client-side using JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`SaveReport`". |
| `sender` | The identifier of the component that triggered this event can have the following values - `"Designer"` |
| `report` | The current report object. |
| `fileName` | The name of the report file for saving. |
| `autoSave` | A flag indicating whether the report is being saved automatically (value `true`) or manually by pressing the save button (value `false`). |
| `preventDefault` | A flag that provides the ability to stop further processing of the event by the designer. The default value is `true`. |

The table below lists the properties passed in the event arguments on the server-side using PHP. The arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, which for this event has the value `StiEventType::SaveReport`. |
| `sender` | The component that triggered this event, which can have the following types: - `StiDesigner` |
| `report` | The current report object. |
| `fileName` | The name of the report file for saving. |
| `autoSave` | A flag indicating whether the report is being saved automatically (value `true`) or manually by pressing the save button (value `false`). |

### onSaveAsReport

[+] JavaScript  [+] PHP


The event is triggered when saving a report in the designer. Detailed descriptions and usage examples can be found in the [Saving a Report](Saving_Report.md) section.


The table below lists the properties passed in the event arguments on the client-side using JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`SaveAsReport`". |
| `sender` | The identifier of the component that triggered this event can have the following values - `"Designer"` |
| `report` | The current report object. |
| `fileName` | The name of the report file for saving. |
| `preventDefault` | A flag that provides the ability to stop further processing of the event by the designer. The default value is `false`. |

The table below lists the properties passed in the event arguments on the server-side using PHP. The arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, which for this event has the value `StiEventType::SaveAsReport`. |
| `sender` | The component that triggered this event, which can have the following types: - `StiDesigner` |
| `report` | The current report object. |
| `fileName` | The name of the report file for saving. |

### onPreviewReport

[+] JavaScript  [+] PHP


The event is triggered when switching to the report preview tab. Detailed descriptions and usage examples can be found in the [Preview](Preview.md) section.


The table below lists the properties passed in the event arguments on the client-side using JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`PreviewReport`". |
| `sender` | The identifier of the component that triggered this event can have the following values - `"Designer"` |
| `report` | The current report object. |
| `viewer` | The current object of the `StiViewer` component embedded in the designer. |
| `preventDefault` | A flag that provides the ability to stop further processing of the event by the designer. The default value is `true`. |

The table below lists the properties passed in the event arguments on the server-side using PHP. The arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, which for this event has the value `StiEventType::PreviewReport`. |
| `sender` | The component that triggered this event, which can have the following types: - `StiDesigner` |
| `report` | The current report object. |

**onCloseReport**

[+] JavaScript  [+] PHP


The event is triggered after the report is closed from the designer menu and before the report has been unassigned from the report designer.
The table below lists the properties passed in the event arguments on the JavaScript client-side:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value `"CloseReport"`. |
| `sender` | The identifier of the component that triggered this event can have the following values: - `"Designer"` |
| `report` | The current report object. |
| `preventDefault` | This flag allows you to stop further processing of the event by the viewer. The default value is `true`. |

The table below lists the properties passed in the event arguments on the PHP server-side, the arguments are of type `StiReportEventArgs`:


| **Name** | **Description** |
| --- | --- |
| `event` | The identifier of the current event, which for this event has the value `StiEventType::CloseReport` |
| `sender` | The component that triggered this event, which can have the following types: - `StiDesigner` |
| `report` | The current report object. |

### onExit

[+] JavaScript  [-] PHP


The event is triggered when the **Exit** button is clicked in the designer's main menu.


The table below lists the properties passed in the event arguments on the client-side using JavaScript:


| **Name** | **Description** |
| --- | --- |
| `event` | Current event identifier, has the value "`Exit`". |
| `sender` | The identifier of the component that triggered this event can have the following values - `"Designer"` |
