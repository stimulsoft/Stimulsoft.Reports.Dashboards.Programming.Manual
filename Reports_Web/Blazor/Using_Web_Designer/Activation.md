# Activation

After acquiring a Stimulsoft product, you should activate the license. You can do it by specifying a license key or loading a file with a license key. Below is an example of the **Blazor Designer** component activation.


**Index.razor**

```
@using Stimulsoft.Report
@using Stimulsoft.Report.Blazor
@using Stimulsoft.Report.Web

<StiBlazorDesigner />

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

You can get a license key or download a file with a license key in [a personal account](https://devs.stimulsoft.com/).
