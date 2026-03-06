# Get Started

**Step 1**: Open Visual Studio;


**Step 2**: Click **File** menu, select **New** item, and choose **Project** item;


**Step 3**: Select **ASP.NET Core Web Application** command;


**Step 4**: Click **Next** button;


**Step 5**: Specify the name of this project, location and solution name. For example, **AngularViewer**;


**Step 6**: Click **Create** button;


**Step 7**: Select **Angular** type, set **.NET Core** as a framework and select **ASP.NET Core 3.1** and higher version;


**Step 8**: Uncheck **Configure for  HTTPS** parameter;


**Step 9**: Click **Create** button;


**Step 10**: Install Stimulsoft.Reports.Angular.NetCore NuGet package:

- Select **Manage NuGet Packages ...** command in the context menu of the project;
- Specify **Stimulsoft.Reports.Angular.NetCore** in the search bar on the **Browse** tab;
- Select the item, define the version of the package, and click Install. When updating the package, click the **Update** button.


**Step 11**: Add **ViewerController** to Conntrollers folder:

- Call context menu of **Controllers** folder;
- Select **Add** item;
- Choose **Controller...** command;
- Set **MVC Controller - Empty** as controller type;
- Click **Add** button;
- Specify controller name. For example, **ViewerController**;
- Click the **Add** button.


**Step 12**: Create the **Reports** folder in the project, and add a report file to it. For example, add **MasterDetail.mrt** report.


**Step 13**: Add below code in **ViewerController.cs**.


**ViewerController.cs**

```csharp
...
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Stimulsoft.Report;
using Stimulsoft.Report.Angular;
using Stimulsoft.Report.Web;

namespace AngularViewer.Controllers
    {
    [Controller]
    public class ViewerController : Controller
    {

        //Specify viewer options
        [HttpPost]
        public IActionResult InitViewer()
        {
            var requestParams = StiAngularViewer.GetRequestParams(this);
            var options = new StiAngularViewerOptions();
            options.Actions.ViewerEvent = "ViewerEvent";
            return StiAngularViewer.ViewerDataResult(requestParams, options);
        }

        //ViewerEvent() that will process viewer requests.
        [HttpPost]
        public IActionResult ViewerEvent()
        {
            var requestParams = StiAngularViewer.GetRequestParams(this);

            if (requestParams.Action == StiAction.GetReport)
            {
                var report = StiReport.CreateNewReport();
                var path = StiAngularHelper.MapPath(this, $"Reports/MasterDetail.mrt");
                report.Load(path);
                return StiAngularViewer.GetReportResult(this, report);
            }

            return StiAngularViewer.ProcessRequestResult(this);
        }
    }
}
...
```

**Step 14**: Open project folder in explorer;


**Step 15:** Install Angular Client Components from npm.


|  |
| --- |
| npm install stimulsoft-viewer-angular |


**Step 16**: Close console;


**Step 17**: Delete the **ClientApp** folder;


**Step 18**: Go to the **AngularViewer** folder and open console;


**Step 19**: Enter **ng new** **ClientApp** command in console:


|  |
| --- |
| ng new ClientApp |

**Step 20**: Enter ‘**N**’ to not use routing;


**Step 21**: Select the **CSS** format and click Enter button;


**Step 22**: Close console and go to **ClientApp** folder;


**Step 23**: Open console and download **stimulsoft-viewer-angular**.


|  |
| --- |
| npm install stimulsoft-viewer-angular |

**Step 24**: Close console;


**Step 25**: Open **app.module.ts** file in the editor from "**...ClientApp\src\app\**" directory, and add **StimulsoftViewerModule**. Specify below code in **app.module.ts**:


**app.module.ts**

```typescript
...
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { StimulsoftViewerModule } from 'stimulsoft-viewer-angular';
import { HttpClientModule } from '@angular/common/http';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';

@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule,
        StimulsoftViewerModule
        HttpClientModule,
        BrowserAnimationsModule,
        FormsModule
    ],
    providers: [],
    bootstrap: [AppComponent]
})
export class AppModule { }
...
```

**Step 26**: Open **app.component.html** file in the editor from "**...ClientApp\src\app\**" directory, and add **AppComponent**. Specify below code in **app.component.html**:


**app.component.html**

```html
...
<stimulsoft-viewer-angular
    [requestUrl]="'http://localhost:60801/Viewer/{action}'"
    [action]="'InitViewer'"
    [height]="'600px'"
></stimulsoft-viewer-angular>
...
```

Where:

- **[requestUrl]** is URL to ViewerController with {action} template. You can find out the URL to **ViewerController** in launchSettings.json file from the "**...\Properties**" directory.

- **[action]** is an action name to initialize an angular viewer.
- **[height]** is viewer height.


**Step 27**: Go to the visual studio and run the project. After the project run, you can see the viewer with a specific report.


> **Information**
>
> If your project does not start, try to delete node_modules folder and package-lock.json file from the "**...ClientApp\**" directory.
