# Activation

> **YouTube** [WPF components](https://www.youtube.com/watch?v=_0yZOSEfFVk&list=PL-72PPAq-3SUaNkPsRwmCgtMoXJhW1OzD&index=2)

After purchasing a Stimulsoft product, you need to activate the license for the components you are using. You can do this done in various ways. Below is an example of activating the **WPF** component.


**MainWindows.xaml..cs**

```csharp
...
public partial class MainWindow : Window
{
    public MainWindow()
    {
        //Activation with using license code
        Stimulsoft.Base.StiLicense.Key = "Your activation code...";
        
        //Activation with using license file
        Stimulsoft.Base.StiLicense.LoadFromFile("license.key");
        
        //Activation from byte array
        Stimulsoft.Base.StiLicense.LoadFromBytes(bytes);
        
        //Activation from stream
        Stimulsoft.Base.StiLicense.LoadFromStream(stream);
        
        //Activation from assembly
        Stimulsoft.Base.StiLicense.LoadFromEntryAssembly(assembly, "stimulsoft-license.key");
        
        InitializeComponent();
    }
}
...
```

You can get a license key or download a file with [a license key in the user's account](https://devs.stimulsoft.com/). To log in to your account, please use the username and password specified when purchasing the product.
