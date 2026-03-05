# Connecting Data

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.

Data for rendering a report can be connected in various ways. The easiest way is to store connection settings in the report template. Also, data can be connected from the code. You can do this before assigning the report to the viewer.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{
    DataSet ds = new DataSet();
    ds.ReadXml(Server.MapPath("Reports/Demo.xml"));
    
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Reports/TwoSimpleLists.mrt"));
    report.Dictionary.Databases.Clear();
    report.RegData("Demo", ds);
        
    StiWebViewer1.Report = report;
}
...
```

To connect report data, you can use the special **OnGetReportData** event, which will be called before the report is rendered.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnGetReportData="StiWebViewer1_GetReportData">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_GetReportData(object sender, StiReportDataEventArgs e)
{    
    DataSet dataSet = new DataSet();
    dataSet.ReadXml(Server.MapPath("Reports/Demo.xml"));
    e.Report.RegData(dataSet);
}
...
```

### SQL data sources

The connection parameters to the SQL data source and any other ones can be stored in the report template. Suppose you want to set the connection parameters from the code before rendering the report (for example, for security reasons or depending on the authorized user). In that case, you can use the example below.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnGetReportData="StiWebViewer1_GetReportData">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs**

```csharp
...
protected void StiWebViewer1_GetReportData(object sender, StiReportDataEventArgs e)
{    
    OracleConnection connection = new OracleConnection("Data Source=Oracle8i;Integrated Security=yes");
    connection.Open();
    OracleDataAdapter adapter = new OracleDataAdapter();
    adapter.SelectCommand = new OracleCommand("SELECT * FROM Products", connection);
     
    DataSet dataSet = new DataSet("productsDataSet");
    adapter.Fill(dataSet, "Products");
     
    e.Report.RegData("Products", dataSet);
}
...
```

Also, for SQL data sources used in the report, you can specify the **Query Timeout** in seconds. The value of this property is stored in the report template for each SQL connection separately.


Below is an example of code that you may use to change the connection string for MS SQL, adjust the query, set the query timeout for the already created connection and data sources in the report.


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{ 
    
    StiReport report = new StiReport();
    report.Load(Server.MapPath("Report.mrt"));
    ((StiSqlDatabase)report.Dictionary.Databases["Connection"]).ConnectionString = @"Data Source=server;Integrated Security=True;Initial Catalog=DataBase";
    ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).SqlCommand = "select * from Table where Column = 100";
    ((StiSqlSource)report.Dictionary.DataSources["DataSourceName"]).CommandTimeout = 1000;
    
    StiWebViewer1.Report = report;
}
...
```


> **Information**
>
> For SQL data sources of other types, the connection is created similarly, and an adapter corresponding to the data source type is connected. For example, for the MS SQL data source, you should connect SqlDataAdapter. For OLE DB - OleDbDataAdapter is required. Also, you should specify a connection string that matches the connection type.

You can also use data for designing reports and dashboards obtained from OData storage. In this case, you can do the authorization using a username, user password, or token. Authorization parameters are specified in the connection string to the OData storage using the ";" separator.


**Default.aspx.cs**

```csharp
...
protected void Page_Load(object sender, EventArgs e)
{ 
    
    var report = new StiReport();
    
    //Authorization using a user account        
    var oDataDatabase = new StiODataDatabase("OData", "OData", @"https://services.odata.org/V4/Northwind/Northwind.svc;AddressBearer=adress;UserName=UserName;Password=Password;Client_Id=Your Client ID", false, null);
    
    //Authorization using a user token        
    var oDataDatabase = new StiODataDatabase("OData", "OData", @"https://services.odata.org/V4/Northwind/Northwind.svc;Token=Enter your token", false, null);
    
    report.Dictionary.Databases.Add(oDataDatabase);
    oDataDatabase.Synchronize(report);
    
    //Query with data filter
    ((StiSqlSource)report.Dictionary.DataSources["Products"]).SqlCommand = "Products?$filter=ProductID eq 2";

    StiWebViewer1.Report = report;
}
...
```

The table below shows the connection string templates for different types of data sources.


| **Data Source** | **Samples of Connection Strings** |
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
| MongoDB | mongodb://<user>:<password>@localhost/test |
| OData | http://services.odata.org/v3/odata/OData.svc/ |
| Other... | The table shows the most commonly used templates for the connection string. You can view various connection string options at [the special website](https://www.connectionstrings.com/). |


### Data from XML, JSON, Excel files

Connecting to XML and JSON data sources can be stored in the report template. If you want to specify data files from the code, you can use the example below.


**Default.aspx**

```
...
<cc1:StiWebViewer ID="StiWebViewer1" runat="server"
    OnGetReportData="StiWebViewer1_GetReportData">
</cc1:StiWebViewer>
...
```


**Default.aspx.cs (XML file)**

```
...
protected void StiWebViewer1_GetReportData(object sender, StiReportDataEventArgs e)
{    
    DataSet data = new DataSet();
    data.ReadXml(Server.MapPath("Data/Demo.xml"));
     
    e.Report.RegData(data);
}
...
```


**Default.aspx.cs (JSON file)**

```
...
protected void StiWebViewer1_GetReportData(object sender, StiReportDataEventArgs e)
{    
    DataSet data = StiJsonToDataSetConverterV2.GetDataSetFromFile(Server.MapPath("Data/Demo.json")); 
    
    e.Report.RegData(data);
}
...
```


> **Information**
>
> The viewer has the possibility of obtaining data from an Excel file. To do this, you can use the following method.
>
>
> DataSetdataSet = StiExcelConnector.Get().GetDataSet`(`new StiExcelOptions(array, this.FirstRowIsHeader));
