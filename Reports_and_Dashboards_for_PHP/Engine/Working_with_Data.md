# Working with Data

Typically, connection parameters to data sources are stored within the report template itself—these can be either file data sources or SQL data sources. If data needs to be connected from the code, a special `regData()` method is available for the report object. The method requires two parameters: the name of the data source in the report and the data itself. The data can be in JSON or XML format as a string, as well as in the form of a PHP object or an array.


Example of connecting data as an object:


**index.php**


<?php

use Stimulsoft\Report\StiReport;


$report = new StiReport();


$data = new stdClass();

$data->Customers = [

"CompanyName" => "Centro comercial Moctezuma",

"Address" => "Sierras de Granada 9993",

"Phone" => 12355500,

"ContactTitle" => "Marketing Manager"];


$report->regData("Demo", $data);

$report->render();


$report->process();

?>

In some cases, it may be necessary to synchronize the report’s data dictionary structure with the incoming data. To do this, set the third parameter of the `regData()` method to `true`. This ensures that the data dictionary is synchronized before the report is generated.


**Information**


When using the Designer component, you can create a new report object and pass data to it with dictionary synchronization enabled. In this case, the designer will open with a new report and preloaded data, ready for use.

### Clearing connection parameters and data dictionary

If a loaded report already has configured data connection parameters, they take priority. To enforce the use of a custom dataset, the report object provides a special method called `clearData()`. By default, this method clears only the connection parameters. If you need to completely reset the data dictionary structure (removing all existing data sources), call the method with `true` as a parameter.


Example of connecting data after clearing the existing dictionary:


**index.php**


<?php

use Stimulsoft\Report\StiReport;


$report = new StiReport();


$report->clearData(true);


$data = '{"Customers": [{"CompanyName": "Centro comercial Moctezuma", "Address": "Sierras de Granada 9993", "Phone": 12355500, "ContactTitle": "Marketing Manager"}]}';


$report->regData("Demo", $data, true);

$report->render();


$report->process();

?>

### Pre-render event

To connect data before generating the report or to modify the report itself, you can use the special event `onBeforeRender` of the report object. This event is triggered before the report is generated, right after it is loaded. To connect data, simply call the `regReportData()` method within the event arguments. The parameters of this method are the same as those of the `regData()` method.


Example of connecting data within a report event:


**index.php**


<?php

use Stimulsoft\Report\StiReport;

use Stimulsoft\Events\StiReportEventArgs;


$report = new StiReport();


$report->onBeforeRender = function (StiReportEventArgs $args) {

$data = '{"Customers": [{"CompanyName": "Centro comercial Moctezuma", "Address": "Sierras de Granada 9993", "Phone": 12355500, "ContactTitle": "Marketing Manager"}]}';

$args->regReportData("Demo", $data);

};


$report->render();

$report->process();

?>


**Information**


If the report already contains data set using the `regData()` method of the report object, it will be overridden by the data specified in the event.

**Client-side data connection**

If needed, data can also be connected using JavaScript functions of the report generator. This can be done by using the `onBeforeRender` event of the report object. Data can be directly loaded into a special `DataSet` object, which is used to store it. The `DataSet` contains functions for loading data from XML/XSD and JSON files. After loading the files, you need to call the `regData()` function of the report object to connect the data, passing the prepared `DataSet` object as an argument.


Example of loading data from an XML file using an XSD schema:


**index.php**


<?php

use Stimulsoft\Report\StiReport;


$report = new StiReport();

$report->onBeforeRender = 'beforeRender';

$report->render();

?>


function onBeforeRender(args) {

let dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");

dataSet.readXmlSchemaFile("Demo.xsd");

dataSet.readXmlFile("Demo.xml");


let report = args.report;

report.regData(dataSet.dataSetName, "", dataSet);

report.dictionary.synchronize();

}


**Information**


Data scheme loading is not essential. If you want to use data scheme, you should add it before XML data loading.

Example of loading data from a JSON file:


**index.php**


<?php

use Stimulsoft\Report\StiReport;


$report = new StiReport();

$report->onBeforeRender = 'beforeRender';

$report->render();

?>


function onBeforeRender(args) {

let dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");

dataSet.readJsonFile("Demo.json");


let report = args.report;

report.regData(dataSet.dataSetName, "", dataSet);

report.dictionary.synchronize();

}

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Rendering%20a%20Report%20from%20Code.php).


In addition to the `readXmlFile()` and `readJsonFile()` functions, there are also `readXml()` and `readJson()` functions, which accept data in the form of a string or object.


**Information**


The function `report.dictionary.synchronize()` is necessary for synchronizing the connected data with the report template's data dictionary. When this function is called, the report dictionary will be created based on the structure of the data loaded into the `DataSet`. The synchronization function is not required if the dictionary is pre-created and its structure matches the connected data.
