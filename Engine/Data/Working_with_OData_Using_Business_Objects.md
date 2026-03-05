# Working with OData Using Business Objects

The protocol **Open Data (OData)** is used to access from different sources, including relational databases, file systems, content management systems and ordinary web sites. **OData** realizes the **CRUD** conception (Create, Read, Update, Delete) in relation to data. In **Visual Studio 2010** and **.NET Framework 4.0** was simplified with support of **OData** using the access technology **Entity Framework**. On the basis of received (using OData protocol) data, it is possible for a user to create reports. Passing data to the report goes through business objects. Let’s have an example of retrieving data from the report and passing data to the report:

  * Connect the **Stimulsoft** assemblies;

  * Add **Service Reference** specifying the address of the entry point to OData-Service. In this case the address is http://services.odata.org/V3/OData/OData.svc;

  * Use following code.


**C#**

```csharp
...
//Connecting to Data Storage
Uri uri = new Uri("http://services.odata.org/V3/OData/OData.svc");
var container = new ServiceReference1.DemoService(uri);

//Creating Query with Selection Parameters
var product = container.Products.Where(p => p.ID < 50).ToList();

//Transffering Data to Report via Business Objects
var report = var StiReport();
report.RegBusinessObject("Products", product);
report.Dictionary.SynchronizeBusinessObjects(2);
report.Design();
...
```
