# Report Engine

The reporting tool [Stimulsoft Reports.PYTHON](https://www.stimulsoft.com/en/products/reports-python) allows you to download, build and export a report in various formats without deploying a viewer and designer. This allows you to avoid loading a large number of scripts on the client side and increases the speed and ease of operation.


The report is built and exported on the client side using JavaScript; the Python server side contains everything needed to work with report files and communicate with various SQL data sources. Communication between the client and the server is carried out through AJAX requests that transmit and receive JSON data in a specific format. For ease of use of the product, special events and functions have been developed both on the JavaScript client side and on the Python server side.


### Dashboards

The dashboard tool [Stimulsoft Dashboards.PYTHON](https://www.stimulsoft.com/en/products/dashboards-python) allows loading and analyze data, exporting and printing analytical panels to various formats without deployment of the viewer and designer.


All data analysis, except for certain SQL operations, is performed on the client side using JavaScript; the Python server-side contains everything needed to work with dashboard files and communicate with various SQL data sources. The client communicates with the server in exactly the same way as in the reporting tool; the same events and functions are used. The Python server-side is universal for dashboards and reports, the same events and functions apply.

* [Usage](Usage.md)
* [Connecting data files](Connecting_Data_Files.md)
* [Optimizing scripts loading](Optimazing_scripts_loading.md)
* [Working with report variables](Connecting_SQL_Data.md)
* [License activation](Activation.md)
* [Working with report variables](Using_Variables.md)
* [Loading and saving reports](Loading_and_Saving_Report.md)
* [Connecting custom fonts](Conneting_Custom_Fonts.md)
* [Report rendering](Rendering_Report.md)
* [Printing a report from code](Printing_from_Code.md)
* [Rendering a report on server side](../Rendering_Report_on_Server_Side.md)
* [Exporting a report from code](Export_from_Code.md)
* [Event handler](Handler.md)
* [Report engine events](Events.md)
* [Working with data](Working_with_Data.md)
