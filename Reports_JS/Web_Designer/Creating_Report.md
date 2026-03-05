# Creating New Report

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

No action is required to run the designer with a new (empty) report. When the component is loaded, the new report will be created automatically. If you need, you can create a new report object and preload the data for it, or perform some other necessary actions.

**designer.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
//var  newDashboard = Stimulsoft.Report.StiReport.createNewDashboard();

report.reportName = "MyNewReport";
//newDashboard.reportName = "MyDashboard";
...
```


A special **DataSet** object is used for data storage, which has a set of methods for loading data from various formats. The **regData()** method is used to connect the data to the report. The arguments of the method indicate the prepared **DataSet** object.

**designer.html**

```html
...
report.regData(dataSet);
...
```

Data is added to a special collection of the report object, and is used to build it. Data structure synchronization is used to display the structure of the registered data in the report dictionary. The **synchronize()** method is used for this.


**designer.html**

```html
...
report.dictionary.synchronize();
...
```

You can also create a new report using the main menu of the designer. The **onCreateReport** event is used to load data for a new report, or to perform some other necessary actions. This event will be called when you create a new empty report, or when you create a report using the wizard.


**designer.html**

```html
...
designer.onCreateReport = function (args) {
    var dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
    dataSet.readJsonFile("Data/Demo.json");
    
    args.report.regData(dataSet.dataSetName, "", dataSet);
    args.report.dictionary.synchronize();
}
...
```

Also, you can pre-create a connection to the data source of the selected type, and add it to the collection of connections in the report template. This method is similar to creating a connection in the report dictionary using the designer interface.


**designer.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
//var  newDashboard = Stimulsoft.Report.StiReport.createNewDashboard();

var xmlDataBase = new Stimulsoft.Report.Dictionary.StiXmlDatabase("Demo", "Demo.xsd", "Demo.xml");

report.loadFile("SimpleList.mrt");
//newDashboard.loadFile("Dashboard.mrt");
report.dictionary.databases.clear();
//newDashboard.dictionary.databases.clear();
report.dictionary.databases.add(xmlDataBase);
//newDashboard.dictionary.databases.add(xmlDataBase);
...
```


In this way, you can add the required number of data sources of different types.
