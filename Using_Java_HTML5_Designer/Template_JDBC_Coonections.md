# Template JDBC Coonections

***.mrt**

```
...
jdbc.driver={myDriver};
jdbc.url={myConnectionUrl};
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```

An example for a **SQLServer****:**


***.mrt**

```
...
jdbc.driver=com.microsoft.sqlserver.jdbc.SQLServerDriver;
jdbc.url= jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]];
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```


[https://msdn.microsoft.com/en-us/library/ms378428](https://msdn.microsoft.com/en-us/library/ms378428)

An example for a **Oracle****:**


***.mrt**

```
...
jdbc.driver=oracle.jdbc.driver.OracleDriver;
jdbc.url=jdbc:oracle:thin:@[HOST][:PORT]:SID;
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```


[https://www.orafaq.com/wiki/JDBC](https://www.orafaq.com/wiki/JDBC)

An example for a **POSTGreSQL****:**


***.mrt**

```
...
jdbc.driver= org.postgresql.Driver
jdbc.url= jdbc:postgresql://[host]:[port]/[database]
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```


http://jdbc.postgresql.org/documentation/80/connect.html
