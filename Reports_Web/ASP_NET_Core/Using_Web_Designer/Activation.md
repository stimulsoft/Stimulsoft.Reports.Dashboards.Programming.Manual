# Activation

> **YouTube**
>
> Watch videos which show how to activate the [ASP.NET Core HTML5 Designer](https://www.youtube.com/watch?v=y6-Vjr5oLPU). Subscribe to the [Stimulsoft channel](https://www.youtube.com/user/StimulsoftVideos) to find out about the new video lessons uploaded. Leave your questions and suggestions in the comments to the video.

After purchasing a Stimulsoft product, you need to activate the license for the components you are using. You can do this by specifying a license key or by downloading a file with the license key. Below is an example of activating the **StiNetCoreDesigner** component.


**HomeController.cs**

```csharp
...
//Activation with using license code
public class HomeController : Controller
{
    static HomeController()
    {
        Stimulsoft.Base.StiLicense.Key = "Your activation code...";
    }
}

//Activation with using license file
public class HomeController : Controller
{
    public HomeController(IHostingEnvironment hostEnvironment)
    {
        var path = Path.Combine(hostEnvironment.ContentRootPath, "Content\\license.key");
        Stimulsoft.Base.StiLicense.LoadFromFile(path);
    }
...
```

You can get a license key or download a file with [a license key in the user's account](https://devs.stimulsoft.com/). To log in to your account, please use the username and password specified when purchasing the product.
