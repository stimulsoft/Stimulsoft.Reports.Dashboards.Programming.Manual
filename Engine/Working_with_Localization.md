# Working with Localization

In Stimulsoft, the `StiLocalization` class is used to load, store, modify, and retrieve localized strings. This class supports loading localizations from XML files, streams, embedded assembly resources, and can automatically select a localization based on the current system culture. However, there are differences in the properties and methods of the `StiLocalization` class between the report generators for the [.NET](#netengine) and [JavaScript](#jsengine) platforms.


### .NET Engine

The following properties and methods are available for working with localizations.


### DirectoryLocalization Property

Provides the ability to specify the name of the folder where localization XML files are stored. The default value is `Localization`.


**C#**

```csharp

StiLocalization.DirectoryLocalization = "Localization";
```

### Localization Property

Provides the ability to specify the name of the localization file.


**C#**

```csharp

StiLocalization.Localization = "zh-CHS.xml";
```

### SearchLocalizationFromRegistry Property

Provides the ability to search for the path to the localization folder in the operating system registry.


**C#**

```csharp

StiLocalization.SearchLocalizationFromRegistry = true;
```

### Language, Description, and CultureName Properties

Provide access to the localization name, description, and culture code after a localization has been loaded.


**C#**

```csharp

StiLocalization.LoadCurrentLocalization();
Console.WriteLine(StiLocalization.CultureName);
```

### IsEn, IsDe, IsBeRu, and IsCyrillic Properties

Provide the ability to determine the type of the loaded localization.


**C#**

```csharp

if (StiLocalization.IsDe) Console.WriteLine("German locale");
```

### BlockLocalizationExceptions and BlockLocalizationLoading Properties

Provide control over localization loading behavior and error handling. They can be used to suppress exceptions when localization keys are missing or to completely disable the loading of localization files.


**C#**

```csharp

StiLocalization.BlockLocalizationExceptions = true; // Disables exceptions for missing localization keys
StiLocalization.BlockLocalizationLoading = false; // Enables localization loading
```

### GetDirectoryLocalizationFromRegistry() Method

Provides the ability to retrieve the path to the localization directory stored in the operating system registry. If registry-based lookup is disabled or the directory does not exist, the method returns `null`.


**C#**

```csharp

string path = StiLocalization.GetDirectoryLocalizationFromRegistry();
```

### GetDirectoryLocales() Method

Provides the ability to locate a `locales` directory next to the application's executable file. The method returns the path only if the directory contains localization XML files.


**C#**

```csharp

string path = StiLocalization.GetDirectoryLocales();
```

### GetEnumValue(string key) Method

Provides the ability to retrieve a localized enumeration value from the `PropertyEnum` category.


**C#**

```csharp

string value = StiLocalization.GetEnumValue("AlignmentCenter");
```

### LoadDefaultLocalization() Method

Provides the ability to load the built-in English localization from the assembly resources.


**C#**

```csharp

StiLocalization.LoadDefaultLocalization();
```

### LoadCurrentLocalization() Method

Provides the ability to load the current localization. If the `Localization` property is specified, the corresponding file is loaded. Otherwise, the method attempts to select a localization based on the current operating system culture.


**C#**

```csharp

StiLocalization.LoadCurrentLocalization();
```

### Load(string file) Method

Provides the ability to load a localization from an XML file.


**C#**

```csharp

StiLocalization.Load(@"Localization\de.xml");
```

**Load(Stream stream) Method**
Provides the ability to load a localization from a stream.


**C#**

```csharp

using var stream = File.OpenRead("pt.xml");
StiLocalization.Load(stream);
```

**GetParam(string file, ...) Method**
Provides the ability to retrieve localization information (language, description, and culture) without fully loading the localization file.


**C#**

```csharp

StiLocalization.GetParam("ko.xml", out var language, out var description, out var cultureName);
```

**GetParam(Stream stream, ...) Method**
Provides the ability to retrieve localization information from a stream.


**C#**

```csharp

StiLocalization.GetParam(stream, out var language, out var description, out var cultureName);
```

**Add(string category, string key, string value) Method**
Provides the ability to add a new localization value or update an existing one.


**C#**

```csharp

StiLocalization.Add("MainMenu", "File", "NewFile");
```

**Get(string category, string key) Method**
Provides the ability to retrieve a localized string by category and key. If the specified value is not found, an exception is thrown.


**C#**

```csharp

string text = StiLocalization.Get("MainMenu", "File");
```

**GetCleaned(string category, string key) Method**
Provides the ability to retrieve a localized string after additional processing by the `Loc.GetCleaned()` method.


**C#**

```csharp

string text = StiLocalization.GetCleaned("MainMenu", "File");
```

**GetValue(string category, string key) Method**
An alias of the `Get(category, key)` method. Provides the ability to retrieve a localized string by category and key. If the value is not found, an exception is thrown.


**C#**

```csharp

string text = StiLocalization.GetValue("MainMenu", "File");
```

**Get(string category, string key, bool throwError) Method**
Provides the ability to retrieve a localized string. Allows exception generation to be disabled when the specified category or key is not found.


**C#**

```csharp

string text = StiLocalization.Get("MainMenu", "UnknownKey", false);
```

**Set(string category, string key, string value) Method**
Provides the ability to modify a localization value in memory.


**C#**

```csharp

StiLocalization.Set("MainMenu", "File", "App File");
```

**GetKeys(string category) Method**
Provides the ability to retrieve a list of all keys in the specified category.


**C#**

```csharp

string[] keys = StiLocalization.GetKeys("MainMenu");
```

**GetValues(string category) Method**
Provides the ability to retrieve a list of all values in the specified category.


**C#**

```csharp

string[] values = StiLocalization.GetValues("MainMenu");
```

**GetCategories() Method**
Provides the ability to retrieve a list of all categories in the loaded localization.


**C#**

```csharp

string[] categories = StiLocalization.GetCategories();
```

**GetLocalization(bool format) Method**
Provides the ability to retrieve the current localization in JSON format.


**C#**

```csharp

string json = StiLocalization.GetLocalization(true);
```

### JS Engine

The following properties and methods are available for working with localizations.


**cultureName Property**
Provides the ability to get or set the code of the current localization.


**JavaScript**

```javascript

StiLocalization.cultureName = "de";
console.log(StiLocalization.cultureName);
```

**loadLocalizationFile(filePath) Method**
Provides the ability to load a localization from a file.


**JavaScript**

```javascript

StiLocalization.loadLocalizationFile("locales/de.xml");
```

**get(category, key) Method**
Provides the ability to retrieve a localized string by category and key. If the value is not found, the method returns the value of the `key` parameter.


**JavaScript**

```javascript

const text = StiLocalization.get("MainMenu", "File");
```

**getJsonStringLocalization() Method**
Provides the ability to retrieve the current localization in JSON format.


**JavaScript**

```javascript

const json = StiLocalization.getJsonStringLocalization();
```

**setLocalization(localizationXml, onlyThis) Method**
Provides the ability to load a localization from an XML string. If the `onlyThis` parameter is set to `true`, the list of registered localizations is cleared.


**JavaScript**

```javascript

StiLocalization.setLocalization(localizationXml);
```

**loadLocalization(localizationXml) Method**
Provides the ability to load a localization from an XML string and returns the name of the loaded language.


**JavaScript**

```javascript

const language = StiLocalization.loadLocalization(localizationXml);
```

**addLocalizationFile(filePath, load, language) Method**
Provides the ability to register a localization file. If the `load` parameter is set to `true`, the localization is loaded immediately.


**JavaScript**

```javascript

StiLocalization.addLocalizationFile("locales/de.xml");
```

**setLocalizationFile(filePath, onlyThis) Method**
Provides the ability to set the current localization from the specified file. If the `onlyThis` parameter is set to `true`, the list of registered localizations is cleared.


**JavaScript**

```javascript

StiLocalization.setLocalizationFile("locales/fr.xml");
```
