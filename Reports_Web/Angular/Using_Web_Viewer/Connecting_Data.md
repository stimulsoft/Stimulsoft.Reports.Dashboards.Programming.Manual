# Connecting Data

Data to a report can be connected in various ways. The easiest way is to store connection settings in the report template. You can also connect the data from the code, this can be done when the report is loaded in the **GetReport** action.


**HomeController.cs**

```csharp
...
public IActionResult GetReport()
{
    DataSet ds = new DataSet();
    ds.ReadXml(StiAngularHelper.MapPath(this, "Data/Demo.xml"));
    
    StiReport report = new StiReport();
    report.Load(StiAngularHelper.MapPath(this, "Reports/TwoSimpleLists.mrt"));
    report.Dictionary.Databases.Clear();
    report.RegData("Demo", ds);
    
    return StiAngularViewer.GetReportResult(this, report);
}
...
```

Data for the report can be connected not only when the report is loaded. For example, you can connect new data at the moment of interactive actions in the viewer (applying report parameters, sorting, drill-down, collapsing). To do this, you should set the **Interaction** action for the **Angular Viewer** component, and, in the action handler, connect the data for the current report. The same way you can connect data in other actions of the viewer.


**HomeController.cs**

```csharp
...
public IActionResult InitViewer()
{
    var requestParams = StiAngularViewer.GetRequestParams(this);
    var options = new StiAngularViewerOptions();
    options.Actions.ViewerEvent = "ViewerEvent";
    options.Actions.Interaction = "ViewerInteraction";
    
    return StiAngularViewer.ViewerDataResult(requestParams, options);
}
...
```


**HomeController.cs**

```csharp
...
public IActionResult ViewerInteraction()
{ 
    DataSet data = new DataSet();
    data.ReadXml(StiAngularHelper.MapPath(this, "Data/Demo.xml"));
    
    StiReport report = StiAngularViewer.GetReportObject(this);
    report.RegData("Demo", data);
    
    return StiAngularViewer.InteractionResult(this, report);
}
...
```

If you want to connect new data only for a certain interactive action of the viewer, for example, only when you apply report parameters, you can use the parameters of the viewer. The viewer parameters are represented as an object of the **StiRequestParams** class, they are passed to any server side on any request, and contain all necessary information and states of the client part of the viewer. To determine the type of the action of the viewer, it is enough to check the **Action** property of the viewer parameters.


**HomeController.cs**

```csharp
...
public IActionResult ViewerInteraction()
{
    StiRequestParams requestParams = StiAngularViewer.GetRequestParams(this);
    if (requestParams.Action == StiAction.Variables)
    {
        DataSet data = new DataSet();
        data.ReadXml(StiAngularHelper.MapPath(this, "Data/Demo.xml"));
        
        StiReport report = StiAngularViewer.GetReportObject(this);
        report.RegData("Demo", data);
        
        return StiAngularViewer.InteractionResult(this, report);
    }
    
    return StiAngularViewer.InteractionResult(this);
}
...
```

### SQL data sources

The connection parameters to the SQL data source, as well as to any other ones, can be stored in the report template. If you want to set the connection parameters from the code before rendering the report (for example, for security reasons or depending on the authorized user), you can use the example below.


**HomeController.cs**

```csharp
...
public IActionResult GetReport()
{
    OracleConnection connection = new OracleConnection("Data Source=Oracle8i;Integrated Security=yes");
    connection.Open();
    OracleDataAdapter adapter = new OracleDataAdapter();
    adapter.SelectCommand = new OracleCommand("SELECT * FROM Products", connection);
     
    DataSet dataSet = new DataSet("productsDataSet");
    adapter.Fill(dataSet, "Products");
     
    StiReport report = new StiReport();
    report.Load(StiAngularHelper.MapPath(this, "Reports/SqlSampleReport.mrt"));
    report.RegData("Products", dataSet);
    
    return StiAngularViewer.GetReportResult(this, report);
}
...
```

Also, for SQL data sources used in the report, you can specify the Query Timeout in seconds. The value of this property is stored in the report template for each SQL connection separately.


Below is an example of code that you may use to change the connection string for MS SQL, adjust the query, set the query timeout for the already created connection, and data sources in the report.


**HomeController.cs**

```csharp
...
public IActionResult GetReport()
{ 
    
    StiReport report = new StiReport();
    report.Load(StiAngularHelper.MapPath("Report.mrt"));
    ((StiSqlDatabase)report.Dictionary.Databases["Connection"]).ConnectionString = @"Data Source=server;Integrated Security=True;Initial Catalog=DataBase";
    ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).SqlCommand = "select * from Table where Column = 100";
    ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).CommandTimeout = 1000;
    
    return StiAngularViewer.GetReportResult(this, report);
}
...
```


> **Information**
>
> For SQL data sources of other types, the connection is created similarly, and an adapter corresponding to the type of the data source is connected. For example, for the MS SQL data source, you should connect SqlDataAdapter, for OracleDataAdapter is required for Oracle. Also, you should specify a connection string that matches the connection type.

The table below shows the connection string templates for different types of data sources.


| **Data Source** | **Connection String Template** |
| --- | --- |
| MS SQL | Integrated Security=False; Data Source=myServerAddress;Initial Catalog=myDataBase; User ID=myUsername; Password=myPassword; |
| MySQL | Server=myServerAddress; Database=myDataBase;UserId=myUsername; Pwd=myPassword; |
| ODBC | Driver={SQL Server}; Server=myServerAddress;Database=myDataBase; Uid=myUsername; Pwd=myPassword; |
| OLE DB | Provider=SQLOLEDB.1; Integrated Security=SSPI;Persist Security Info=False; Initial Catalog=myDataBase;Data Source=myServerAddress |
| Oracle | Data Source=TORCL;User Id=myUsername;Password=myPassword; |
| MS Access | Provider=Microsoft.Jet.OLEDB.4.0;User ID=Admin;Password=pass;Data Source=C:\\myAccessFile.accdb; |
| PostgreSQL | Server=myServerAddress; Port=5432; Database=myDataBase;User Id=myUsername; Password=myPassword; |
| Firebird | User=SYSDBA; Password=masterkey; Database=SampleDatabase.fdb;DataSource=myServerAddress; Port=3050; Dialect=3; Charset=NONE;Role=; Connection lifetime=15; Pooling=true; MinPoolSize=0;MaxPoolSize=50; Packet Size=8192; ServerType=0; |
| SQL CE | Data Source=c:\MyData.sdf; Persist Security Info=False; |
| SQLite | Data Source=c:\mydb.db; Version=3; |
| DB2 | Server=myAddress:myPortNumber;Database=myDataBase;UID=myUsername;PWD=myPassword;Max Pool Size=100;Min Pool Size=10; |
| Infomix | Database=myDataBase;Host=192.168.10.10;Server=db_engine_tcp;Service=1492;Protocol=onsoctcp;UID=myUsername;Password=myPassword; |
| Sybase | Data Source=myASEserver;Port=5000;Database=myDataBase;Uid=myUsername;Pwd=myPassword; |
| Teradata | Data Source=myServerAddress;User ID=myUsername;Password=myPassword; |
| VistaDB | Data Source=D:\folder\myVistaDatabaseFile.vdb4;Open Mode=ExclusiveReadWrite; |
| Universal(dotConnect) | Provider=Oracle;direct=true;data source=192.168.0.1;port=1521;sid=sid;user=user;password=pass |
| MongoDB | mongodb://&lt;user&gt;:&lt;password&gt;@localhost/test |
| OData | http://services.odata.org/v3/odata/OData.svc/ |


> **Information**
>
> The table shows the most commonly used templates for the connection string. You can view various connection string options at [the special website](https://www.connectionstrings.com/).


### Data from XML, JSON, Excel files

Connecting to XML and JSON data sources can be stored in the report template. If you want to specify data files from the code, you can use the example below.


**HomeController.cs**

```csharp
...
public IActionResult GetReport()
{
    DataSet data = new DataSet();
    data.ReadXml(StiAngularHelper.MapPath(this, "Data/Demo.xml"));
    
    StiReport report = new StiReport();
    report.Load(StiAngularHelper.MapPath(this, "Reports/SimpleList.mrt"));
    report.RegData(data);
    
    return StiAngularViewer.GetReportResult(this, report);
}
...
```


**HomeController.cs**

```csharp
...
public IActionResult GetReport()
{
    DataSet data = StiJsonToDataSetConverterV2.GetDataSetFromFile(StiAngularHelper.MapPath(this, "Data/Demo.json"));
    
    StiReport report = new StiReport();
    report.Load(StiAngularHelper.MapPath(this, "Reports/SimpleList.mrt"));
    report.RegData(data);
    
    return StiAngularViewer.GetReportResult(this, report);
}
...
```


> **Information**
>
> The viewer has the possibility of obtaining data from an Excel file. To do this, you can use the following method.
>
>
> DataSet dataSet = StiExcelConnector.Get().GetDataSet`(`newStiExcelOptions(array, this.FirstRowIsHeader));
