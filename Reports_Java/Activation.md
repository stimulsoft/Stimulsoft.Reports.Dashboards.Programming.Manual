# Activation

After purchasing a Stimulsoft product, you need to activate the license for the components you are using. You can do this by specifying a license key or by downloading a file with the license key. Below is an example of activating the **StiWebViewer** component.


**index.jsp**

```
...
<body>
    <%
        //Activation with using license code
        com.stimulsoft.base.licenses.StiLicense.setKey(
        "Your activation code...";

        //Activation with using license file
        com.stimulsoft.base.licenses.StiLicense.loadFromFile(request.getSession().getServletContext().getRealPath("/license/license.key"));
    %>
    <stiwebviewer:webviewer report="${report}" options="${options}" />
</body>
...
```

You can get a license key or download a file with [a license key in the user's account](https://devs.stimulsoft.com/). To log in to your account, please use the username and password specified when purchasing the product.
