# Installation and Description HTML5 Designer

**Create a sample page with report webdesigner**

Create a simple page with a report webdesigner. To do this, put the following libraries into the **WebContent\WEB-INF\lib\** directory: stimulsoft.lib.jar, stimulsoft.reports-base.jar, stimulsoft.reports-report.jar, stimulsoft.reports-flex.jar, stimulsoft.reports-web.jar, stimulsoft.reports-webdesigner.jar .


Next, edit **web.xml** it should look like in Listing 1:


**web.xml**

```xml
...
<?xml version="1.0" encoding="UTF-8" ?>
    <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="http://java.sun.com/xml/ns/javaee" xmlns:web="http://java.sun.com/xml/ns/javaee/webapp_2_5.xsd"
        xsi:schemaLocation="http://java.sun.com/xml/ns/javaee"
        id="WebApp_ID" version="2.5">
    <display-name>sti_webdesigner</display-name>
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
        <!-- configuration, this parameter indicates the main application directory -->
    <servlet>
        <servlet-name>StimulsoftResource</servlet-name>
        <servlet-class>com.stimulsoft.web.servlet.StiWebResourceServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>StimulsoftResource</servlet-name>
        <url-pattern>/stimulsoft_web_resource/*</url-pattern>
    </servlet-mapping>
    <servlet>
        <servlet-name>StimulsoftDesignerAction</servlet-name>
        <servlet-class>com.stimulsoft.webdesigner.servlet.StiWebDesignerActionServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>StimulsoftDesignerAction</servlet-name>
        <url-pattern>/stimulsoft_webdesigner_action</url-pattern>
    </servlet-mapping> 
</web-app>
...
```

Leave unchanged the remaining web.xml blocks, which defines the servlets required for working. Then, edit the index.jsp (Listing 2).


**index.jsp**

```
...
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<%@page import="java.io.FileOutputStream"%>
<%@page  import="java.io.FileInputStream"%>
<%@page  import="com.stimulsoft.report.utils.data.StiDataColumnsUtil"%>
<%@page  import="com.stimulsoft.report.dictionary.StiDataColumnsCollection"%>
<%@page  import="com.stimulsoft.report.dictionary.StiDataColumn"%>
<%@page  import="com.stimulsoft.report.utils.data.StiSqlField"%>
<%@page  import="com.stimulsoft.report.dictionary.dataSources.StiDataTableSource"%>
<%@page  import="com.stimulsoft.report.utils.data.StiXmlTable"%>
<%@page  import="com.stimulsoft.report.utils.data.StiXmlTableFildsRequest"%>
<%@page  import="com.stimulsoft.webdesigner.StiWebDesigerHandler"%>
<%@page  import="com.stimulsoft.webdesigner.StiWebDesignerOptions"%>
<%@page 
    import="com.stimulsoft.report.dictionary.databases.StiXmlDatabase"%>
<%@page  import="java.io.File"%>
<%@page  import="com.stimulsoft.report.StiSerializeManager"%>
<%@page  import="com.stimulsoft.report.StiReport"%>
<%@page  language="java" contentType="text/html; charset=utf-8"
    pageEncoding="UTF-8"%>
<%@taglib uri="http://stimulsoft.com/webdesigner" prefix="stiwebdesigner"%>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Stimulsoft Webdesigner for Java</title>
    <style type="text/css">
    </style>
</head>
<body>
    <%
        final String reportPath = request.getSession().getServletContext().getRealPath("/reports/Master-Detail.mrt");
        final String xmlPath = request.getSession().getServletContext().getRealPath("/data/Demo.xml");
        final String xsdPath = request.getSession().getServletContext().getRealPath("/data/Demo.xsd");
        final String savePath = request.getSession().getServletContext().getRealPath("/save/");
            
        StiWebDesignerOptions options = new StiWebDesignerOptions();                
        StiWebDesigerHandler handler = new StiWebDesigerHandler(){
            public StiReport getEditedReport(HttpServletRequest request){
                try{
                    StiReport report = StiSerializeManager.deserializeReport(new File(reportPath));
                    report.getDictionary().getDatabases().add(new StiXmlDatabase("Demo", xsdPath, xmlPath));
                    return report;
                } catch (Exception e){
                        e.printStackTrace();
                }
                return null;
            }
            
            public void onOpenReportTemplate(StiReport report, HttpServletRequest request){
                report.getDictionary().getDatabases().add(new StiXmlDatabase("Demo", xsdPath, xmlPath));
            }
            
            public void onNewReportTemplate(StiReport report, HttpServletRequest request){
                report.getDictionary().getDatabases().add(new StiXmlDatabase("Demo", xsdPath, xmlPath));
                try{
                    // In new report if you want to use wizard, you must populate report with datasources   
                    StiXmlTableFildsRequest tables = StiDataColumnsUtil.parceXSDSchema(new FileInputStream(xsdPath));
                    for (StiXmlTable table : tables.getTables()){
                        StiDataTableSource tableSource = new StiDataTableSource("Demo." + table.getName(), table.getName(), table.getName());
                        tableSource.setColumns(new StiDataColumnsCollection());
                        for (StiSqlField field : table.getColumns()){
                            StiDataColumn column = new StiDataColumn(field.getName(), field.getName(), field.getSystemType());
                            tableSource.getColumns().add(column);
                        }
                        tableSource.setDictionary(report.getDictionary());
                        report.getDictionary().getDataSources().add(tableSource);   
                    }                    
                } catch (Exception e){
                    e.printStackTrace();   
                }                
            }
                    
            public void onSaveReportTemplate(StiReport report, StiRequestParams requestParams, HttpServletRequest request) {
                try {
                    FileOutputStream fos = new FileOutputStream(savePath + requestParams.designer.fileName);
                    if (requestParams.designer.password != null) {
                        StiSerializeManager.serializeReport(report, fos, requestParams.designer.password);
                    } else {
                        StiSerializeManager.serializeReport(report, fos, true);
                    }
                    fos.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        };       
        pageContext.setAttribute("handler", handler);
        pageContext.setAttribute("options", options);
    %>

<stiwebdesigner:webdesigner
    handler="${handler}" options="${options}" />
</body>
</html>
...
```

Add taglib directives in the JSP. They will work with custom tags on the page.

### Listing 3. Custom Stimulsoft tag


**index.jsp**

```
...
<%@ taglib uri="http://stimulsoft.com/webdesigner" prefix="stiwebdesigner"%>
...
```

Add a tag  `<stiwebdesigner:resources />`, tag used to load necessary resources (css & js) for webdesigner, it haven’t any attributes, it must be placed inside HTML <head> tag.

### Description of webdesigner tag


**web.xml**

```xml
...
<stiwebdesigner:webdesigner handler="${handler}" report="${report}" />
...
```

This tag contains next attributes:

* **handler** [required] – com.stimulsoft.webdesigner.StiWebDesigerHandler object to handle webdesigner;

* **options** [optional] – StiWebdesignerOptions object to customize webdesigner. If not present – default options are used;

* **designerID** [optional] – String value identifier of webdesigner HTML element. If more than one webdesigner present in HTML page each webdesigner must have different identifier.

### Description of StiWebDesigerHandler


To handle designer events, class that implement **StiWebDesigerHandler** must be created and setup in stiwebdesigner tag. Occured on opening {@link StiReport}.


* **public StiReport getEditedReport(HttpServletRequest request)**;

Occurred on loading webdesinger. Here must present implementation of loading report and population it with Database\Data sources (if required).


* **public void onOpenReportTemplate(StiReport report, HttpServletRequest request)**;

Occurred on opening StiReport. Method intended for populate report with Database\Data sources (if required).


* **public void onNewReportTemplate(StiReport report, HttpServletRequest request);**

Occurred on new StiReport. Method intended for populate report with Database\Data sources (if required).

In new report if you want to use wizard, you must populate report with datasources.


* **public void onSaveReportTemplate(StiReport report, String reportName, HttpServletRequest request);**

Occurred on save StiReport. Method must implement saving StiReport.
