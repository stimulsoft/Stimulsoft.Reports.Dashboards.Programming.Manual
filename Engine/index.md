# Engine

> **Information**
>
> A report can contain sub reports. By default, if the calculation mode of the main (calling) report is set to **Interpretation**, all nested reports will also be processed in this mode. However, if the calculation mode of the main report is set to **Compilation**, the nested reports will be processed according to their own calculation mode.
>
>
> However, it is possible to allow sub reports to be executed in **Compilation** mode regardless of the calculation mode of the main report. To do this, set the `AllowOpenSubReportWithCompilation` option to `true`. For example: `StiOptions.Engine.AllowOpenSubReportWithCompilation = true;`

In this chapter you can read questions related to the capabilities of the report engine.


* [Data](Data/index.md)
* [Exports](Exports/index.md)
* [Report Inheritance](Report_Inheritance/index.md)
* [Scripts](Scripts/index.md)
* [Right to Left](Right_to_Left/index.md)
