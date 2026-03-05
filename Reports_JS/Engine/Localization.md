# Localization

The **HTML5 Viewer** **and** **HTML5 Designer** components support full localization of the user interface. The special static method - **addLocalizationFile()** - is used to localize the report viewer interface to the required language. As the arguments of the method, you should specify the path to the localization XML file, and specify whether the localization will automatically load together with the component.


The specified function adds localization to the designer menu:


**index.html**

```html
...
Stimulsoft.Base.Localization.StiLocalization.addLocalizationFile("../localization/de.xml", true);
...
```

The specified function adds localization to the designer menu, but doesn`t load it automatically:


**index.html**

```html
...
Stimulsoft.Base.Localization.StiLocalization.addLocalizationFile("../localization/de.xml", false, "Deutsch");
...
```

After the method is called, a link to a localization file will be added to the internal collection. The file will be loaded the first time you select the specified localization in the designer menu. It saves memory and time of components run. In this variant, you should specify localization name for displaying in the designer menu as the third argument. After localization loaded this value will be taken from a localization file.


The specified function adds localization to the designer menu and sets it by default:


**index.html**

```html
...
Stimulsoft.Base.Localization.StiLocalization.setLocalizationFile("../localization/de.xml");
...
```

When each the designer loading, this localization will be selected even if earlier another localization was selected.


> **Information**
>
> For the **HTML5 Designer****,** when creating a project with pure JavaScript, the necessary localization files should be added using the above code. If the project uses the Node.js technology, then it is enough to specify a folder with localization files. In this case all the files in it will be added automatically:
>
> Stimulsoft.System.NodeJs.localizationPath = "locales";
