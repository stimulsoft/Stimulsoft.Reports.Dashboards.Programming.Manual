# Get Started for ASP.NET Core 3.1

1. Create the **ASP.NET Core Empty** application;
2. Install the **Stimulsoft.PDF.Forms** component into the application from the **NuGet** package manager;
3. In **Startup.cs**, configure the application to use controllers:


**Startup.cs**

```csharp

public void ConfigureServices(IServiceCollection services)
{       
    services.AddControllers();
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseDefaultFiles();
    app.UseStaticFiles();
    
    app.UseRouting();

    app.UseCors(builder => builder.AllowAnyOrigin().AllowAnyHeader().AllowAnyMethod());

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
            name: "default",
            pattern: "{controller=Forms}/{action=Action}");
    });
}
```

1. Create the **Controllers** folder;
2. Add **FormsController.cs** to the **Controllers** folder, which will process requests from the **Stimulsoft PDF Forms** component:


**FormsController.cs**

```csharp

public class FormsController : Controller
{        
    [HttpPost]
    public IActionResult Action()
    {
        try
        {
            var data = JObject.Parse(this.HttpContext.Request.Form["data"]);
            var action = data["action"].ToString();
            switch (action)
            {
                case "Initialize":
                    var initData = StiWebForm.Initialize(data, null);
                    return Json(initData.Content);               
            
                default:
                    var result = StiWebForm.ProcessRequest(data);
                    return result.ContentType switch
                    {
                        "application/pdf" => new FileContentResult(result.Content as byte[], result.ContentType),
                        _ => Json(result.Content),
                    };
            }
        }
        catch (Exception e)
        {
            return new ContentResult()
            {
                Content = e.Message,
                ContentType = "text/plain"
            };    
        }
    }
}
```

1. Inside the application folder, run the command in the terminal to create a new **Angular** application with no `routing` and CSS styling:


**console**

ng new sti-forms-designer --routing false --style css

1. Rename the **sti-forms-designer** folder to **ClientApp**;
2. In the **package.json** file, add dependencies for **Stimulsoft PDF Forms** and the necessary components:


**package.json**

```json

"stimulsoft-forms": "^2024.2.4",
"ngx-color-picker": "^13.0.0",
"primeicons": "^6.0.1",
"primeng": "^14.1.2",
"resize-observer-polyfill": "^1.5.1",
"rxjs": "~6.5.0"
```

1. Add styles to the **angular.json** file and improve the `budgets`:


**angular.json**

```json

"build": {
    "options": {
        "styles": [
            "src/styles.css",
            "node_modules/primeicons/primeicons.css",
            "node_modules/primeng/resources/primeng.min.css",
            "node_modules/stimulsoft-forms/theme.css"
        ]},
        
        "configurations": {
            "production": {
                "budgets": [
                    {
                        "type": "initial",
                        "maximumWarning": "500kb",
                        "maximumError": "5mb"
                    }]
                }   
            }
        }
    }
}
```

1. Update the imports in **ClientApp\src\app\app.module.ts**:


**app.module.ts**

```typescript

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from "@angular/forms";
import { HttpClientModule } from "@angular/common/http";
import { BrowserAnimationsModule } from "@angular/platform-browser/animations";
import { DropdownModule } from "primeng/dropdown";
import { StimulsoftFormsModule } from 'stimulsoft-forms';
import { AppComponent } from './app.component';


@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule,
        HttpClientModule,
        FormsModule,
        BrowserAnimationsModule,
        DropdownModule,
        StimulsoftFormsModule
    ],
    providers: [],
    bootstrap: [AppComponent]
})
```

1. Update **ClientApp\src\app\app.component.ts**:


**app.component.ts**

```typescript

import { Component } from '@angular/core';
import { StimulsoftFormsService } from 'stimulsoft-forms';

@Component({
    selector: 'app-root',
    template: `
        <stimulsoft-forms
            [requestUrl]="'http://localhost:7536/Forms/Action'" /*URL to Forms controller, you can find this url in launchSettings.json file of the project*/
            [form]="form" /*StiForm object to use to create form object using StimulsoftFormsService*/
            [style.width]="'100%'"
            [style.height]="'100%'">
        </stimulsoft-forms>
`
})

export class AppComponent {
    public form!: any;

    constructor(public formService: StimulsoftFormsService) {
        this.form = this.formService.createElement("Form");
    }
}
```

1. Update **ClientApp\src\app\index.html**:


**index.html**

```html

<!doctype html>
<html lang="en" style="position: fixed;width:100%;height:100%">
<head>
    <meta charset="utf-8">
    <title>StiFormsDesigner</title>
    <base href="/">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body style="width:100%;height:100%">
    <app-root></app-root>
</body>
</html>
```

1. Go to the **ClientApp** folder;
2. Run the command to install **Angular** components:


**console**

npm i --force

1. Run the command to build an **Angular** application:


**console**

ng build --output-hashing none

1. Create the **wwwroot** folder in the project's root folder;
2. Copy all files from **ClientApp\dist\sti-forms-designer\** into **wwwroot**;
3. Run the project.
