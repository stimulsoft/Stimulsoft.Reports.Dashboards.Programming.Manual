## Connecting SQL Databases

> **Information**
>
> Since dashboards and reports use the same unified template format - MRT, methods for loading the template and working with data, the word “report” will be used in the documentation text.


> **Samples**
>
> See examples on GitHub [how to connect to databases](https://github.com/stimulsoft/Samples-Reports.JS-for-Node.js/tree/master/Starting%20SQL%20adapters%20from%20the%20HTTP%20server).

Since pure JavaScript does not have built-in methods for working with remote databases, this functionality is implemented using server-side code. Therefore, Stimulsoft Reports.JS product contains server data adapters implemented using Node.js, PHP, .NET, .NET Core, Python, Java technologies. The database adapter is a software layer between the DBMS and the client script. The adapter connects to the DBMS and retrieves the necessary data, converting it into JSON. The script running on the server (using the adapter) provides for the exchange of JSON data between the client-side JavaScript application and the server side. To use this mechanism on the client side, you should specify the URL address of the host adapter, which processes requests to a required adapter


Links to examples with ready [data adapters](https://github.com/stimulsoft/DataAdapters.JS), implemented for various platforms: Node.js, PHP, .NET, .NET Core, Python, Java.


It`s easy to use an adapter. You should run an adapter and specify the its address:


**index.html**

```html
...
StiOptions.WebServer.url = "http://localhost:9615";
...
```


When requesting data from SQL data sources, the Stimulsoft.Report.Engine sends a POST request to the URL, specified in the option:


**index.html**

```html
...
StiOptions.WebServer.url = "https://localhost/handler.php";
...
```

A JSON object with parameters is passed in the body of the request that use the following structure:

* **command**: two variants are possible - "TestConnection" and "ExecuteQuery";

* **connectionString**: database connection string;

* **queryString**: query string;

* **database**: database type;

* **timeout**: the time of request waiting, specified in the data source;

* **parameters**: an array of parameters as a JSON object {name, value};

* **escapeQueryParameters**: a flag of parameters shielding before requesting.

In response, the Stimulsoft.Report.Engine expects a JSON object with data in the form of the following structure:

* **success**: a flag of successful command execution;

* **notice**: if the flag of command execution has the **false** value, this parameter will contain an error description;

* **rows**: strings array, each element is the array of values, the index is the column number;

* **columns**: an array of column names, index is the column number;

* **types**: an array of column types, the index is the column number. It can take the values "string", "number", "int", "boolean", "array", "datetime".

Request and response sample:


**index.html**

```html
...
request = {
    command: "ExecuteQuery",
    connectionString: "Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;",
    queryString: "select * from table1",
    database: "MS SQL"
}

response = {
    success: true,

    rows: [
        ["value1", 1, false],
        ["value2", 1, true]
        ["value3", 2, false]
    ],
    columns: [
        "Column1_name",
        "Column2_name",
        "Column3_name"
    ],
    types:[
        "string",
        "int",
        "boolean"
    ]
}
...
```

### Custom Data Base

Also, you may register custom data base. To do it you should invoke the following option:


**index.html**

```html
...
Stimulsoft.Report.Dictionary.StiCustomDatabase.registerCustomDatabase(options);
...
```

The options are the set of properties and the process() function, which will be invoked when requesting data:

* **serviceName**: adapter name which will be displayed in the designer when creating a new connection

* **designerCategory**:  the category name to which the adapter will be added in the **New Data Source** menu. By default, the adapter can be found in the `Favorites` category, but you can change this by setting the option to one of the following values: `"Files"`, `"SQL"`, `"NoSQL"`, `"Azure"`, `"Google"`, `"OnlineServices"`, `"REST"`.

* **sampleConnectionString**: the sample of a connection string that is inserted in the form of setting up a new connection

* **process**: the function, which will be invoked to prepare and transmit data to the Stimulsoft.Report.Engine


Two arguments are transmitted to the input of the **process()** function: **command** and **callback**.


The **command** argument is the JSON object, where the Stimulsoft.Report.Engine will transfer the following parameters:

* **command**: action, which is being invoked at the moment. Possible values: "**TestConnection**": test the database connection from the new connection creation form "**RetrieveSchema**": retrieving data schema is needed to optimize a request and not only to transfer necessary data set. It is invokes after connection creation "**RetrieveData**": data request.

* **connectionString**: connection string;

* **queryString**: query string;

* **database**: database type;

* **timeout**: the time of request waiting, specified in the data source.


The **callback** argument is the function, which should be invoked to transmit prepared data to the Stimulsoft.Report.Engine. As the callback argument to the functions you must pass a JSON object with the following parameters:

* **success**: the flag of successful command execution;

* **notice**: if the flag of command execution has the **false** value, this parameter should contain an error description;

* **rows**: strings array, each element is the array from values, the index is the column number;

* **columns**: columns name array, the index is the column number;

* **types**: the object where field name is column name and the value is the type of the column {Column_Name : "string"}. The type can take the following values "string", "number", "int", "boolean", "array", "datetime". If the **columns** array will be transmitted, you will be able to transmit types array to the **types**, the index should be column number. It doesn't work for the "**RetrieveSchema**".


If the command = "**RetrieveSchema**", then in addition types you should transmit table names to the **types**.

The sample of a request and response when receiving a schema:


**index.html**

```html
...
request = {
    command: "RetrieveSchema"
}

response = {
    success: true,
    
    types:{
        Table1: {
            Column1: "string",
            Column2: "number"
        },
        Table2: {
            Column1: "string"
        }
    }
}
...
```

The sample of a request and response when getting data:


**index.html**

```html
...
request = {
    command: "RetrieveData",
    queryString: "Table1"
}
response = {
    success: true,
   
    rows: [
        ["value1", 1],
        ["value2", 1]
        ["value3", 2]
    ],
    columns:[
        "Column1",
        "Column2"
    ],
    types:[
        "string",
        "number"
    ]
}
...
```

[The example of adapter registration](https://github.com/stimulsoft/Samples-Reports.JS-for-HTML/blob/main/Working%20with%20Designer/Using%20a%20Custom%20Data%20Adapter.html).

**Query Timeout**

Also, for SQL data sources used in the report, you can specify the **Query Timeout** in seconds. The value of this property is stored in the report template for each SQL connection separately.


Below is an example of code that you may use to change the connection string for MS SQL, adjust the query, set the query timeout for the already created connection, and data sources in the report.

**index.html**

```html
...
var report = new Stimulsoft.Report.StiReport();
report.loadFile("Report.mrt");
report.dictionary.databases.getByName("Connection").connectionString = "Data Source=server;Integrated Security=True;Initial Catalog=DataBase";
report.dictionary.dataSources.getByName("DataSourceName").sqlCommand = "select * from Table where Column = 100";
report.dictionary.dataSources.getByName("DataSourceName").commandTimeout = 1000;
...
```


> **Information**
>
> The address to the data adapter must be set before the creation code of the component or the report object, since the value of this option must be known to the report engine before it is initialized.
>
> The following SQL data sources are currently supported - MySQL, MS SQL, PostgreSQL, Firebird, and Oracle. The data adapters are open source and can be modified the way you need.

### OData storages

You can also use data for designing reports and dashboards obtained from OData storages. In this case, you can do the authorization using a username, user password, or using a token. Authorization parameters are specified in the connection string to the OData storage using the ";" separator.


**viewer.html**

```html
...
//Authorization using a user account
var oDataDatabase = new Stimulsoft.Report.Dictionary.StiODataDatabase("OData", "OData", "https://services.odata.org/V4/Northwind/Northwind.svc;AddressBearer=adress;UserName=UserName;Password=Password;Client_Id=Your Client ID", false, null);

//Authorization using a user token
var oDataDatabase = new Stimulsoft.Report.Dictionary.StiODataDatabase("OData", "OData", "https://services.odata.org/V4/Northwind/Northwind.svc;Token=Enter your token", false, null);

report.dictionary.databases.add(oDataDatabase);
report.dictionary.synchronize();

//Query with data filter
var productsDataSource = report.dictionary.dataSources.getByName("Products");
if (productsDataSource != null) productsDataSource.sqlCommand = "Products?$filter=ProductID eq 2";
...
```

Also, you can specify user HTTP headers for data sources. It can be done in the `onBeginProcessData` event handler. A complete [sample is available on our website](https://www.stimulsoft.com/en/samples/search?searchword=Supply%20Custom%20Headers%20for%20JSON%20Database):


**index.html**

```html
...
// In `onBeginProcessData` event handler add custom HTTP headers
report.onBeginProcessData = function (args) {
    if (
        args.database === "JSON" &&
        args.command === "GetData" &&
        args.pathData && args.pathData.include("/reports/ProtectedDemo.json")
    ) {
        // Add custom header to pass through backend server protection
        args.headers.push({key: "X-Auth-Token", value: "*YOUR TOKEN*"});
    }
};
...
```
