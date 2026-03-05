# Activation

> **YouTube** [ASP.NET HTML5 Designer](https://www.youtube.com/watch?v=0WH7nLSIPC4&list=PL-72PPAq-3SXIABu0QnUsTtNxoMxVyXsQ&index=1)

After purchasing a Stimulsoft product, you need to activate the license for the components you are using. You can do this by specifying a license key or by downloading a file with the license key. Below is an example of activating the **StiWebDesigner** component.


**Default.aspx.cs**

```csharp
...
public partial class _Default : Page
{
    static _Default()
    {
        //Activation with using license code
        Stimulsoft.Base.StiLicense.Key = "Your activation code...";
        
        //Activation with using license file
        var path = HttpContext.Current.Server.MapPath("license.key");
        Stimulsoft.Base.StiLicense.LoadFromFile(path);
    }
}
...
```

You can get a license key or download a file with [a license key in the user's account](https://devs.stimulsoft.com/). To log in to your account, please use the username and password specified when purchasing the product.
