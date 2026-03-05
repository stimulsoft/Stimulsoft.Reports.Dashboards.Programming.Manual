# Activation

> **YouTube** [WinForms components](https://www.youtube.com/watch?v=7wQSqpcCMSI&list=PL-72PPAq-3SWXBf9Pq7NeUVVCv-FDc1Q7&index=4)

After purchasing a Stimulsoft product, you need to activate the license for the components you are using. You can do this done in various ways. Below is an example of activating the **WinForms** component.


**Form1.cs**

```csharp
...
public partial class Form1 : Form
{
    public Form1()
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
