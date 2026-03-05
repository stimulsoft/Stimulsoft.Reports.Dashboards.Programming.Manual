## How to Show Report

Add the following code to display the rendered report (*.mdc, *.mdz, *.mdx):


**XAML**

```
...
<Page x:Class="Demo.RT.BlankPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"xmlns:viewerRT="using:Stimulsoft.Report.Viewer.RT"><viewerRT:StiViewerControl x:Name="viewerControl"/>
</Page>
...
```


**C#**

```csharp
...
namespace Demo.RT
{
    public sealed partial class BlankPage : Page
    {
        #region Handlers
        async private void BlankPage_Loaded(object sender, RoutedEventArgs e)
        {
            StorageFolder folder = Windows.Storage.KnownFolders.DocumentsLibrary;
            StorageFile storageFile = await folder.GetFileAsync("SimpleList.mdc");
            
            StiReport report = new StiReport();
            await report.LoadDocumentAsync(storageFile);
            viewerControl.Report = report;
        }
        #endregion

        public BlankPage()
        {
            this.InitializeComponent();
            this.Loaded += BlankPage_Loaded;
        }
    }
}
...
```

If the report has not been rendered, i.e. the report template is saved (*.mrt, *.mrz, *.mrx), then enter the following code:


**XAML**

```
...
<Page x:Class="Demo.RT.BlankPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"xmlns:viewerRT="using:Stimulsoft.Report.Viewer.RT"><viewerRT:StiViewerControl x:Name="viewerControl"/>
</Page>
...
```


**C#**

```csharp
...
namespace Demo.RT{
    public sealed partial class BlankPage : Page
    {
        #region Handlersasync private void BlankPage_Loaded(object sender, RoutedEventArgs e){
            StorageFolder folder = Windows.Storage.KnownFolders.DocumentsLibrary;StorageFile storageFile = await folder.GetFileAsync("SimpleList.mrt");StiReport report = new StiReport();await report.LoadAsync(storageFile);await report.RenderAsync();viewerControl.Report = report;
        }#endregionpublic BlankPage(){
            this.InitializeComponent();this.Loaded += BlankPage_Loaded;
        }
    }
}
...
```

You can open a rendered report by clicking the **Open** button.
