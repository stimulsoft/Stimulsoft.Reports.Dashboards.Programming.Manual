# Angular JS

This chapter describes an example of using Stimulsoft components in Angular JS applications.


**Create an Angular project**
In the terminal navigate to the directory where you want to place the new project. Then, run the command.


**terminal**

ng new sti-angular-js --no-standalone --routing --ssr=false --style css

**Install Stimulsoft components**

First, you need to download the Stimulsoft package. If you need reporting tools, you should download the [Stimulsoft Reports.JS](https://www.stimulsoft.com/ru/downloads#reports) package. If you need reporting tools and dashboards, you should download the [Stimulsoft Dashboards.JS](https://www.stimulsoft.com/ru/downloads#dashboards) package. Then, copy the Stimulsoft scripts into the project at the path `sti-angular-js./src/scripts`.

### Configure the Angular project

To do this, in the `scripts` section of the **angular.json** file, you should specify an array of paths to the scripts files in the project.


**angular.json

          ...
          "scripts": [
          "src/scripts/stimulsoft.reports.engine.js",
          "src/scripts/stimulsoft.reports.export.js",
          "src/scripts/stimulsoft.reports.chart.js",
          "src/scripts/stimulsoft.reports.maps.js",
          "src/scripts/stimulsoft.reports.import.xlsx.js",
          "src/scripts/stimulsoft.viewer.js",
          "src/scripts/stimulsoft.designer.js",
          "src/scripts/stimulsoft.blockly.editor.js"
          ]
          ...**

In the section `architect` for the parameter `builder`, set the type to `browser` instead of `application`. Additionally, rename the parameter in `options` from `browser` to `main`.


**angular.json

          ...
          "architect": {
          "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
          "main": "src/main.ts"
          }
          }
          }...**

If you plan to use pre-existing reports in the viewer or designer, you should add the path to them in the `assets` section.


**angular.json

          ...
          "assets": [
          "src/reports"
          ]...**

**Add the HttpClientModule module**
You need to import and then connect the `HttpClientModule` in the `app.module.ts` file.


**app.module.ts

          import { HttpClientModule } from '@angular/common/http';
          
          @NgModule({
          ...
          imports: [
          BrowserModule,
          AppRoutingModule,
          HttpClientModule
          ],
            ...
          })**

**Place the Stimulsoft component**
In the **app.component.ts** file, you also need to import `HttpClientModule`. Then, you can import Stimulsoft using the directive `declare var Stimulsoft: any;`. In the `AppComponent` class, you should define the initialization of Stimulsoft components. For example, the designer with an empty report.


**app.component.ts

          import { Component } from '@angular/core';
          import { HttpClientModule } from '@angular/common/http';
          
          declare var Stimulsoft: any;
          
          @Component({
          selector: 'app-root',
          template: `<div>
          <h2>Stimulsoft Reports.JS - Invoice.mrt - Designer</h2>
          <div id="сontent"></div>
          </div>`
          })
          
          export class AppComponent {
          designer: any = new Stimulsoft.Designer.StiDesigner(false, "StiDesigner", false);
          
            ngOnInit() {
          var report = new Stimulsoft.Report.StiReport();
          
          this.designer.report = report;
          this.designer.renderHtml("сontent");
          }
          
          constructor(private http: HttpClientModule) {
          
          }
          }**

Or open the viewer with a previously created report.


**index.html

          ...
          export class AppComponent {
          viewer: any = new Stimulsoft.Viewer.StiViewer(false, "StiViewer", false);
          
            ngOnInit() {
          var report = new Stimulsoft.Report.StiReport();
          report.loadFile("reports/Invoice.mrt");
          
          this.viewer.report = report;
          this.viewer.renderHtml("сontent");
          }
          
          constructor(private http: HttpClientModule) {
          
          }
          }
          ...**

**First Start**
An Angular application by default defines the start command in the **package.json** file. Therefore, to start the project, run the command from the terminal in the root folder of the project.


**console**

npm start
