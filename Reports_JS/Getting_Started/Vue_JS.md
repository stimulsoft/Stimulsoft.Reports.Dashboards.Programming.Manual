# Vue JS

This part describes an example of using Stimulsoft components in Vue applications.


**Create a Vue project**
In the terminal navigate to the directory where you want to place the new project. Then, run the following command.


**terminal**

npm create vue@latest my-app

The application settings can be left as default or modified if necessary.

**Install Stimulsoft components**

First, you need to download the Stimulsoft package. If you need reporting tools, you should download the [Stimulsoft Reports.JS](https://www.stimulsoft.com/ru/downloads#reports) package. If you need reporting tools and dashboards, you should download the [Stimulsoft Dashboards.JS](https://www.stimulsoft.com/ru/downloads#dashboards) package. For this, run the following command.

**terminal**

npm install stimulsoft-dashboards-js

**Integrate Stimulsoft into the application**
To do this, edit the **App.vue** file in the project's **src** folder. First, import the Stimulsoft module and the `onMounted()` method. You can also modify the `template` and `styles` blocks here. Pass a `callback` function with the initialization of Stimulsoft components into the `onMounted()` method. For example, the report designer will open with a blank report.


**App.vue**

```
<script setup lang="ts">
    import { onMounted } from "vue";
    import { Stimulsoft } from "stimulsoft-dashboards-js/Scripts/stimulsoft.designer.js";
    
    onMounted(() => {
        let designer = new Stimulsoft.Designer.StiDesigner(false, "StiDesigner", false);
        let report = new Stimulsoft.Report.StiReport();
        
        designer.report = report;
        designer.renderHtml("content");
    });
</script>

<template>
    <div id="app">
        <div>
            <h2 id="app-title">Stimulsoft Vue JS</h2>
            <div id="content"></div>
        </div>
    </div>
</template>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        margin-top: 60px;
    }
    
    #app-title {
        text-align: center;
    }
</style>
```

Alternatively, open the viewer with a previously created report. The report files should be copied beforehand into the **reports** folder in the **./public** directory of the project.


**App.vue

          ...
          <script setup lang="ts">
          import { onMounted } from "vue";
          import { Stimulsoft } from "stimulsoft-dashboards-js/Scripts/stimulsoft.viewer.js";
          
          onMounted(() => {
          let viewer = new Stimulsoft.Viewer.StiViewer(false, "StiViewer", false);
          let report = new Stimulsoft.Report.StiReport();
          report.loadFile("reports/SimpleList.mrt");
          
          viewer.report = report;
          viewer.renderHtml("content");
          });
          </script>
          ...**

**First Start**
By default, a Vue application defines the start command in the **package.js**on file. Therefore, to run the project, simply execute the command from the terminal in the project's root folder.


**console**

npm run dev
