# Loading, Saving and Loading Custom Data

Before running, the application should be configured. For configuration the my.servlet.ApplicationInitializer class that is specified in the web.xml is used. The code init reports:


**web.xml**

```xml
...
package my.servlet;

import java.io.IOException;
import java.util.Properties;

import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;

import my.actions.MyLoadAction;
import my.actions.MyLoadDataAction;
import my.actions.MyLocalizationAction;
import my.actions.MyMailAction;
import my.actions.MyRenderReportAction;
import my.actions.MySaveAction;

import com.stimulsoft.base.exception.StiException;
import com.stimulsoft.flex.StiFlexConfig;

/**
 * Application initialization.
 */
public class ApplicationInitializer implements ServletContextListener {

    @Override
    public void contextInitialized(final ServletContextEvent event) {
        try {
                // configuration application
                StiFlexConfig stiConfig = initConfigWithoutDir();
                // ---------------------------------------------------------
                // need to override the standard methods
                // another comment
                stiConfig.setLoadClass(MyLoadAction.class);
                stiConfig.setSaveClass(MySaveAction.class);
                stiConfig.setLoadDataClass(MyLoadDataAction.class);
                stiConfig.setMailAction(MyMailAction.class);
                stiConfig.setLocalizationAction(MyLocalizationAction.class);
                stiConfig.setRenderReportAction(MyRenderReportAction.class);
                // ---------------------------------------------------------
                
                StiFlexConfig.init(stiConfig);
                
                // set variable in servlet context attribute
                // Map<String, String> myVariableMap = new HashMap<String, String>();
                // myVariableMap.put("Variable1", "myVariableMap");
                // event.getServletContext().setAttribute("myMap", myVariableMap);
            } catch (Exception e) {
                throw new RuntimeException(e);
            }
    }

    @Override
    public void contextDestroyed(final ServletContextEvent event) {
        // empty
    }

    public StiFlexConfig initConfigWithoutDir() throws StiException, IOException {
        Properties properties = new Properties();
        // load your own Properties;
        // InputStream inStream = getClass().getResourceAsStream("RESOURCE_PATH");
        // properties.load(inStream);
        return new StiFlexConfig(properties);
    }
}
...
```

In which the main application directory with the file stimulsoft.properties will be defined. In order to make your own reports saving or loading, it is necessary to specify these classes in a configuration, just the same way as you can specify a class to load data from xml. Classes are as follow: Listing MyLoadAction.java


**web.xml**

```xml
...
package my.actions;

import java.io.InputStream;

import com.stimulsoft.flex.StiLoadAction;
import com.stimulsoft.flex.utils.StiSaveLoadFileReport;

public class MyLoadAction extends StiLoadAction {

    @Override
    public InputStream load(String repotrName) {
        System.out.println("must override this method to specify your own load repotr");
        return new StiSaveLoadFileReport().getReport(repotrName);
    }
}
...
```

Listing MySaveAction.java:


**web.xml**

```xml
...
package my.actions;

import com.stimulsoft.flex.StiSaveAction;
import com.stimulsoft.flex.utils.StiOperationResult;
import com.stimulsoft.flex.utils.StiSaveLoadFileReport;

public class MySaveAction extends StiSaveAction {

    @Override
    public StiOperationResult save(String report, String reportName, boolean newReportFlag) {
        System.out.println("must override this method to specify your own save report");
        return new StiSaveLoadFileReport().save(report, reportName, newReportFlag);
    }

}
...
```

Listing MyLoadDataAction.java:


**web.xml**

```xml
...
package my.actions;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Properties;

import com.stimulsoft.flex.StiLoadDataAction;

public class MyLoadDataAction extends StiLoadDataAction {

    @Override
    protected String getConnectionString() {
        System.out.println("must override this method to specify your own connection string");
        // return
        // "Data Source=localhost\\SQLEXPRESS;Initial Catalog=Mybase;User ID=UserName; Password=Password;";
        return super.getConnectionString();
    }

    @Override
    protected String getUserName() {
        System.out.println("must override this method to specify your own user name");
        // return "UserName";
        return super.getUserName();
    }

    @Override
    protected String getPassword() {
        System.out.println("must override this method to specify your own password");
        // return "Password";
        return super.getPassword();
    }

    @Override
    protected String getQuery() {
        System.out.println("my Query " + super.getQuery());
        return super.getQuery();
    }
    
    @Override
    public Connection getConnection() throws ClassNotFoundException, SQLException {
        System.out.println("must override this method to specify your own connection");
        boolean overrideByConnectionString = getConnectionString() != null
            && getConnectionString().equals("needOverride");
        boolean overrideByDataSource = getDataSourceName() != null
            && getDataSourceName().equals("DataSourceOverride");
        if (overrideByConnectionString || overrideByDataSource) {
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            Properties info = new Properties();
            info.setProperty("user", "test");
            info.setProperty("password", "test");
            String connectionString = "jdbc:sqlserver://localhost\\SQLEXPRESS1:1433;databaseName=mybase;";
            return DriverManager.getConnection(connectionString, info);
        } else {
            return super.getConnection();
        }
    }
}
...
```

Listing MyLocalizationAction.java:


**web.xml**

```xml
...
package my.actions;

import java.io.BufferedInputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

import com.stimulsoft.base.exception.StiException;
import com.stimulsoft.base.utils.StiXmlMarshalUtil;
import com.stimulsoft.flex.StiLocalizationAction;
import com.stimulsoft.flex.StiLocalizationInfo;
import com.stimulsoft.lib.io.StiFileUtil;

public class MyLocalizationAction extends StiLocalizationAction {

    @Override
    public List<StiLocalizationInfo> getLocalizations() throws StiException, FileNotFoundException {
        System.out.println("must override this method to specify your own Localizations");
        List<StiLocalizationInfo> list = new ArrayList<StiLocalizationInfo>();
        File localizationDir = getLocalizationDir();
        if (localizationDir.exists()) {
            Iterator<File> iterateLocalization = StiFileUtil.iterateFiles(localizationDir,
            new String[] { "xml" }, false);
            for (; iterateLocalization.hasNext();) {
                File fileLoc = iterateLocalization.next();
                InputStream is = new BufferedInputStream(new FileInputStream(fileLoc));
                StiLocalizationInfo localization = StiXmlMarshalUtil.unmarshal(is,
                    StiLocalizationInfo.class);
                localization.setKey(fileLoc.getName());
                list.add(localization);
            }
        }
        return list;
    }

    @Override
    protected File getLocalizationDir() {
        System.out.println("must override this method to specify your own LocalizationDir");
        return new File("Localization");
    }

    @Override
    public InputStream getLocalization(String key) throws StiException, FileNotFoundException {
        System.out.println("must override this method to specify your own load Localization");
        File file = new File(getLocalizationDir(), key);
        return new BufferedInputStream(new FileInputStream(file));
    }
}
...
```

Listing MyMailAction.java:


**web.xml**

```xml
...
package my.actions;

import java.util.Properties;

import javax.mail.BodyPart;
import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.Multipart;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeBodyPart;
import javax.mail.internet.MimeMessage;
import javax.mail.internet.MimeMultipart;
import javax.mail.internet.PreencodedMimeBodyPart;

import com.stimulsoft.base.mail.StiMailProperties;
import com.stimulsoft.flex.StiMailAction;
import com.stimulsoft.flex.interactionObject.StiMailData;

/**
 * MyMailAction.
 * 
 * @Copyright Stimulsoft
 * 
 */
public class MyMailAction extends StiMailAction {

    @Override
    public void init(StiMailData mailData, StiMailProperties mailConf) {
        System.out.println("must override this method to specify your own init");
        this.mailData = mailData;
        this.mailConf = mailConf;
        session = getSession();
    }

    @Override
    protected Session getSession() {
        System.out.println("must override this method to specify your own Session");
        Properties props = getProperties();
        return Session.getInstance(props);
    }

    @Override
    protected Properties getProperties() {
        System.out.println("must override this method to specify your own mail Properties");
        Properties props = new Properties();
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.starttls.enable", "true");
        return props;
    }

    @Override
    protected Message getMessage() throws MessagingException {
        System.out.println("must override this method to specify your own mail Message");
        Message message = new MimeMessage(session);
        message.setRecipients(Message.RecipientType.TO, InternetAddress.parse(mailConf.getFrom()));
        message.setRecipients(Message.RecipientType.CC,
            InternetAddress.parse(mailConf.getRecipients()));

        message.setSubject(mailConf.getSubject());
        
        BodyPart text = getTextPart();
        BodyPart body = getFilePart();
        
        Multipart mp = new MimeMultipart();
        mp.addBodyPart(text);
        mp.addBodyPart(body);
        
        message.setContent(mp);
        return message;
    }

    @Override
    protected BodyPart getTextPart() throws MessagingException {
        System.out.println("must override this method to specify your own mail TextPart");
        MimeBodyPart text = new MimeBodyPart();
        text.setText(mailConf.getBody(), "UTF-8", "plain");
        return text;
    }

    @Override
    protected BodyPart getFilePart() throws MessagingException {
        System.out.println("must override this method to specify your own mail FilePart");
        PreencodedMimeBodyPart body = new PreencodedMimeBodyPart("base64");
        body.setFileName(mailData.getFileName());
        body.setContent(mailData.getData(), mailData.getMIMEType());
        return body;
    }

    private Transport getTransport() throws MessagingException {
        System.out.println("must override this method to specify your own mail Transport");
        Transport transport = session.getTransport("smtp");
        transport.connect(mailConf.getHost(), mailConf.getSmtpPort(), mailConf.getUserName(),
            mailConf.getPassword());
        return transport;
    }

    @Override
    public void sendMessage() throws MessagingException {
        System.out.println("must override this method to specify your own send Message");
        Message message = getMessage();
        Transport transport = getTransport();
        transport.sendMessage(message, message.getAllRecipients());
        transport.close();
    }
}
...
```

Listing MyRenderReportAction.java:


**web.xml**

```xml
...
package my.actions;

import java.io.IOException;

import com.stimulsoft.base.exception.StiException;
import com.stimulsoft.flex.StiRenderReportAction;
import com.stimulsoft.report.StiReport;

public class MyRenderReportAction extends StiRenderReportAction {

    @Override
    public StiReport render(StiReport report) throws IOException, StiException {
        System.out.println("must override this method to specify your own render report");
        return report.render();
    }
}
...
```


**Template JDBC connections**

```
...
jdbc.driver={myDriver};
jdbc.url={myConnectionUrl};
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```


**An example for a SQLServer**

```
...
jdbc.driver=com.microsoft.sqlserver.jdbc.SQLServerDriver;
jdbc.url= jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]];
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```


[http://msdn.microsoft.com/en-us/library/ms378428](http://msdn.microsoft.com/en-us/library/ms378428)

**An example for a Oracle**

```
...
jdbc.driver=oracle.jdbc.driver.OracleDriver;
jdbc.url=jdbc:oracle:thin:@[HOST][:PORT]:SID;
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```


[http://www.orafaq.com/wiki/JDBC](http://www.orafaq.com/wiki/JDBC)

**An example for a postgresql**

```
...
jdbc.driver= org.postgresql.Driver
jdbc.url= jdbc:postgresql://[host]:[port]/[database]
jdbc.username={myUserName };
jdbc.password={ myUserPassword };
...
```


http://jdbc.postgresql.org/documentation/80/connect.html
