# React JS

This part describes an example of using Stimulsoft components in React applications.


**Create a React project**
In the terminal, navigate to the directory where you want to place the new project. Then, run the following command.


**terminal**

npx create-react-app my-app

**Install Stimulsoft components**

First, you need to download the Stimulsoft package. If you need reporting tools, you should download the [Stimulsoft Reports.JS](https://www.stimulsoft.com/ru/downloads#reports) package. If you need reporting tools and dashboards, you should download the [Stimulsoft Dashboards.JS](https://www.stimulsoft.com/ru/downloads#dashboards) package. For this, run the following command.

**terminal**

npm install stimulsoft-dashboards-js

**Integrate Stimulsoft into the application**
To do this, edit the **App.js** file in the project's **src** folder. First, you need to import the `Stimulsoft` module and the `React` class. Then, create an `App` class that extends `React.Component`, override the class constructor, the `render(`) and the `componentDidMount()` methods. For example, the report designer will be opened with an empty report.


**App.js**

```javascript
...
import React from 'react';
import { Stimulsoft } from 'stimulsoft-dashboards-js/Scripts/stimulsoft.designer';

class App extends React.Component {
    constructor() {
        super();
        this.designer = new Stimulsoft.Designer.StiDesigner(false, "StiDesigner", false);
    }

    render() {
        return (
                    <div className="App">
                        <h2>Stimulsoft Designer</h2>
                        <div id="сontent"></div>
                    </div>
        );
    }
 
    componentDidMount() {
        var report = new Stimulsoft.Report.StiReport();
        
        this.designer.report = report;
        this.designer.renderHtml("сontent");
    }
}

export default App;
...
```

Alternatively, open the viewer with a previously created report. The report files should be copied beforehand into the **reports** folder in the **./public** directory of the project.


**App.js

          ...
          class App extends React.Component {
          constructor() {
          super();
          this.viewer = new Stimulsoft.Viewer.StiViewer(false, "StiViewer", false);
          }
          
          render() {
          return (
          <div className="App">
          <h2>Stimulsoft Viewer</h2>
          <div id="сontent"></div>
          </div>
          );
          }
           
          componentDidMount() {
          var report = new Stimulsoft.Report.StiReport();
          report.loadFile("reports/Invoice.mrt");
          
          this.viewer.report = report;
          this.viewer.renderHtml("сontent");
          }
          }
          ...**

### First Start

A **React** application by default defines the start command in the **package.json** file. Therefore, to run the project, simply execute the command from the terminal in the project's root folder.


**console**

npm start
