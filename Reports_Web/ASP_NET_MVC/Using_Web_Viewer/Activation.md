# Activation

After purchasing a Stimulsoft product, you need to activate the license for the components you are using. You can do this by specifying a license key or by downloading a file with the license key. Below is an example of activating the **StiMvcViewer** component.


**HomeController.cs**

```csharp
...
public class HomeController : Controller
{
    static HomeController()
    {
        //Activation with using license code
        Stimulsoft.Base.StiLicense.Key = "Your activation code...";
        
        //Activation with using license file
        var path = System.Web.HttpContext.Current.Server.MapPath("~/Content/license.key");
        Stimulsoft.Base.StiLicense.LoadFromFile(path);
    }
}
...
```

You can get a license key or download a file with [a license key in the user's account](https://devs.stimulsoft.com/). To log in to your account, please use the username and password specified when purchasing the product.
