# Connecting Data

Data for report rendering can be connected in various ways. The easiest way is to keep connection settings in a report template. In addition, data can be connected from a code. You can do it before a report is assigned to the viewer.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    //Report object to use in viewer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Load new data from XML file
        var data = new System.Data.DataSet();
        data.ReadXml("Data/Demo.xml");

        //Create and load report template
        var report = new StiReport();
        report.Load("Reports/TwoSimpleLists.mrt");
        report.Dictionary.Databases.Clear();
        report.RegData("Demo", data);
        
        //Assing report object to viewer
        Report = report;
    }
}
```


> **Information**
>
> At this moment, the SQL data resources are supported only for Blazor Server components.

### SQL data sources

The connection parameters to the SQL data source and any other ones can be stored in the report template. Suppose you want to set the connection parameters from the code before rendering the report (for example, for security reasons or depending on the authorized user). In that case, you can use the example below.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    //Report object to use in viewer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        OracleConnection connection = new OracleConnection("Data Source=Oracle8i;Integrated Security=yes");
        connection.Open();
        
        OracleDataAdapter adapter = new OracleDataAdapter();
        adapter.SelectCommand = new OracleCommand("SELECT * FROM Products", connection);
         
        var dataSet = new DataSet("productsDataSet");
        adapter.Fill(dataSet, "Products");

        var report = new StiReport();
        report.Load("Reports/TwoSimpleLists.mrt");
        report.Dictionary.Databases.Clear();
        report.RegData("Products", dataSet);

        //Assing report object to viewer
        Report = report;
    }
}
```

Also, for SQL data sources used in the report, you can specify the Query Timeout in seconds. The value of this property is stored in the report template for each SQL connection separately.


Below is an example of code that you may use to change the connection string for MS SQL, adjust the query, set the query timeout for the already created connection and data sources in the report.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    //Report object to use in viewer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        var report = new StiReport();
        report.Load("Reports/Report.mrt");
        ((StiSqlDatabase)report.Dictionary.Databases["Connection"]).ConnectionString = @"Data Source=server;Integrated Security=True;Initial Catalog=DataBase";
        ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).SqlCommand = "select * from Table where Column = 100";
        ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).CommandTimeout = 1000;
        
        //Assing report object to viewer
        Report = report;
    }
}
```


> **Information**
>
> For SQL data sources of other types, the connection is created similarly, and an adapter corresponding to the data source type is connected. For example, for the MS SQL data source, you should connect SqlDataAdapter. For OracleDataAdapter is required for Oracle. Also, you should specify a connection string that matches the connection type.

You can also use data for designing reports and dashboards obtained from OData storage. In this case, you can do the authorization using a username, user password, or using a token. Authorization parameters are specified in the connection string to the OData storage using the ";" separator.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    //Report object to use in viewer
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        var report = new StiReport();
        
        //Authorization using a user account        
        var oDataDatabase = new StiODataDatabase("OData", "OData", @"https://services.odata.org/V4/Northwind/Northwind.svc;AddressBearer=adress;UserName=UserName;Password=Password;Client_Id=Your Client ID", false, null);
        
        //Authorization using a user token        
        var oDataDatabase = new StiODataDatabase("OData", "OData", @"https://services.odata.org/V4/Northwind/Northwind.svc;Token=Enter your token", false, null);
        
        report.Dictionary.Databases.Add(oDataDatabase);
        oDataDatabase.Synchronize(report);
        
        //Query with data filter
        ((StiSqlSource)report.Dictionary.DataSources["Products"]).SqlCommand = "Products?$filter=ProductID eq 2";
        
        //Assing report object to viewer
        Report = report;
    }
}
```

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
| Other... | The table shows the most commonly used templates for the connection string. You can view various connection string options at [the special website](https://www.connectionstrings.com/). |


### Data from XML, JSON, Excel files

You can keep connections to the XML and the JSON data resources in a report template. If you need to specify data files from a code, you can use the following example.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Load new data from XML file
        var dataSet = new System.Data.DataSet();
        dataSet.ReadXml("Data/Demo.xml");
        
        var report = new StiReport();
        report.Load("Reports/SimpleList.mrt");
        
        //Register data for the report
        report.RegData("Demo", dataSet);
        
        //Assing report object to viewer
        Report = report;
    }
}
```


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer Report="@Report" />

@code
{
    private StiReport Report;
    
    protected override void OnInitialized()
    {
        base.OnInitialized();
        
        //Load new data from JSON file
        var dataSet = StiJsonToDataSetConverterV2.GetDataSetFromFile("Data/Demo.json");
        
        var report = new StiReport();
        report.Load("Reports/SimpleList.mrt");
        
        //Register data for the report
        report.RegData(dataSet);
        
        //Assing report object to viewer
        Report = report;
    }
}
```


> **Information**
>
> There is an option to retrieve data from an Excel file in the viewer. To do this you can use the following method:
>
>
> var`dataSet =`StiExcelConnector`.Get().GetDataSet(`newStiExcelOptions`(array,`this`.FirstRowIsHeader));`
