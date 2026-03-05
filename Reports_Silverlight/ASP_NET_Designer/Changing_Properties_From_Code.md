## Changing Web Designer Properties From Code

The **PreInit** event is used to change **Web designer** properties. This event occurs before initialization of the designer, i.e. before passing Web designer properties to the client part of an application. In other words, to change the Web designer properties from code in it necessary to add the handler to the **PreInit** event. The code below shows how to add the handler to the PreInit event and set the Localization property to en:


**C#**

```csharp
...
protected void StiWebDesignerSL1_PreInit(object sender, StiWebDesignerSL.StiPreInitEventArgs e)
{
    e.WebDesignerSL.Localization = "en";        
}
...
```

Now, when running the **Web designer**, it will be localized in English. For example, we need to change the browser title. By default, the browser title is the value of the **Report Alias** property. If the value is not set then the **Report Name** is taken. To change the browser title it is necessary to add the code below to the event:


**C#**

```csharp
...
protected void StiWebDesignerSL1_PreInit(object sender, StiWebDesignerSL.StiPreInitEventArgs e)
{
    e.WebDesignerSL.BrowserTitle = "Stimulsoft";
}
...
```

Now, when running the Web designer, Stimulsoft word will be shown as a report title.
