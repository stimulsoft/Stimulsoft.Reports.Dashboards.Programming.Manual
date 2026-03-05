# Activation

After acquiring a Stimulsoft product, you should activate the license for used components. You can do it by specifying your license key or loading a file with your license key. Below is an example of the **StiBlazorViewer** component activation.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorViewer />

@code
{
    protected override void OnInitialized()
    {
        //Activation with using license code
        Stimulsoft.Base.StiLicense.Key = "Your activation code...";
        
        //Activation with using license file
        Stimulsoft.Base.StiLicense.LoadFromFile("Content/license.key");
        
        base.OnInitialized();
    }
}
```

You can get a license key or download a file with a license key in the [user's account](https://devs.stimulsoft.com/). To authorize in the user's personal account, you should use a username and password specified when buying a product.
