# Engine

The [Stimulsoft Reports.PHP](https://www.stimulsoft.com/en/products/reports-php) report generator allows loading, building, and exporting a report to various formats without deploying the viewer and designer. This eliminates the need to load large scripts on the client side.


The report building and exporting is done using the JavaScript core on the client side in the web browser window, or on the server side using the universal Node.js platform. The PHP server-side contains everything needed to work with report files and to connect to various SQL data sources. The client-server communication is done via AJAX requests, transmitting and receiving JSON data in a specific format. For ease of use, special events and functions have been developed for both the client-side JavaScript and the PHP server-side.

**Dashboards**

[Stimulsoft Dashboards.PHP](https://www.stimulsoft.com/en/products/dashboards-php) allows loading, analyzing data, and exporting the dashboard to various formats without deploying the viewer and designer.


All data analysis, except for certain SQL operations, is performed using the JavaScript data analyzer on the client side in the web browser window, or on the server side using the universal Node.js platform. The PHP server side is universal for both dashboards and reports, utilizing the same events and functions.

* [Usage](Usage.md)
* [Connecting Data Files](Connecting_Data_Files.md)
* [Optimization of script loading](Optimazing_scripts_loading.md)
* [Connecting SQL Data Adapters](Connecting_SQL_Data.md)
* [Activation](Activation.md)
* [Work with Report Variables](Using_Variables.md)
* [Loading and Saving Report](Loading_and_Saving_Report.md)
* [Connecting Custom Fonts](Connecting_Custom_Fonts.md)
* [Rendering a Report](Rendering_Report.md)
* [Printing Report from Code](Printing_from_Code.md)
* [Rendering a Report on Server-Side](Rendering_Report_on_Server_Side.md)
* [Export Report from Code](Export_from_Code.md)
* [PHP Events Handler](PHP_Handler.md)
* [Engine Events](Events.md)
