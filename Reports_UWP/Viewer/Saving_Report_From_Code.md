## Saving Report From Code

The report can be saved from the project code. Here is an example of the code to save a report:


**XAML**

```
...
<Page x:Class="Demo.RT.BlankPage">
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"xmlns:viewerRT="using:Stimulsoft.Report.Viewer.RT"><viewerRT:StiViewerControl x:Name="viewerControl"/>
</Page>
...
```


**C#**

```csharp
...
namespace Demo.RT{
    public sealed partial class BlankPage : Page{
        #region Handlersasync private void buttonSaveReport_Click(object sender, RoutedEventArgs e)
        {
            StiReport report = new StiReport();
            StorageFolder folder = Windows.Storage.KnownFolders.DocumentsLibrary;
            StorageFile storageFile = await folder.CreateFileAsync("Report1.mdc");

            await report.SaveDocumentAsync(storageFile);
        }#endregionpublic BlankPage(){
            this.InitializeComponent();this.Loaded += BlankPage_Loaded;
        }
    }
}
...
```
