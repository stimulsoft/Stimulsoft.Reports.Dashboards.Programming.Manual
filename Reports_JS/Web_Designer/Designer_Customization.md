# Customizations in Designer

You can add custom controls to the report designer. In this chapter you may find several examples of customizing the report designer.


Adding a button to the **Home** tab.


**designer.html**

```html
...
var designer = new Stimulsoft.Designer.StiDesigner(designerOptions, "StiDesigner", false);
designer.renderHtml("content");

//Example add custom button to home toolbar panel
var homePanel = designer.jsObject.options.homePanel;

//Add buttons group to insert panel. Parameters of GroupBlock(groupName, groupText) method.
var buttonsGroup = designer.jsObject.GroupBlock("buttonsGroup1", "Group1");
var buttonsGroupTable = designer.jsObject.GroupBlockInnerTable();
buttonsGroup.container.appendChild(buttonsGroupTable);

//Add big button to buttons group. Parameters of BigButton(name, groupName, caption, imageName, toolTip, arrow, styles) method.
var customBigButton = designer.jsObject.BigButton("customButton1", null, "Custom Button", " ", "Tooltip for customButton1");
customBigButton.image.src = "https://www.stimulsoft.com/images/blocks/ultimate-buttons/logo.png";

buttonsGroupTable.addCell(customBigButton).style.padding = "2px";

//customBigButton onclick event
customBigButton.action = function () {
    alert("customButton was pressed!");
}

//Add buttonsGroup and separator to customPanel
homePanel.firstChild.addCell(buttonsGroup);
homePanel.firstChild.addCell(designer.jsObject.GroupBlockSeparator());
...
```

Also, you can add a button to the top panel, near the **File** menu.


**designer.html**

```html
...
var designer = new Stimulsoft.Designer.StiDesigner(designerOptions, "StiDesigner", false);
designer.renderHtml("content");

var toolBarRow = designer.jsObject.options.toolBar.firstChild.tr[0];

var customButton = designer.jsObject.ToolButton("customButton1", "Custom Button");

var buttonCell = document.createElement("td");
buttonCell.className = "stiDesignerToolButtonCell";
buttonCell.appendChild(customButton);

//For example insert button to position 3
toolBarRow.insertBefore(buttonCell, toolBarRow.childNodes[3]);

customButton.action = function () {
    alert("Button clicked!");
}
...
```

Below is an example of adding a custom panel in the report designer.


**designer.html**

```html
...
var designer = new Stimulsoft.Designer.StiDesigner(designerOptions, "StiDesigner", false);
designer.renderHtml("content");

var propertiesPanel = designer.jsObject.options.propertiesPanel;

var customPanel = document.createElement("div");
customPanel.jsObject = designer.jsObject;
customPanel.className = "stiDesignerPropertiesPanelInnerContent";
customPanel.style.top = "35px";
customPanel.style.display = "none";
customPanel.style.background = "gray";

propertiesPanel.containers["Custom"] = customPanel;
propertiesPanel.appendChild(customPanel);

var footerTable = propertiesPanel.footer.firstChild;

var tabButton = designer.jsObject.TabButton("CustomTabButton", "PropertiesGridTabs", "Custom");
tabButton.style.margin = "0 0 0 3px";

tabButton.action = function () {
    if (!this.isSelected) propertiesPanel.showContainer("Custom");
}

designer.jsObject.loc.Panels.Custom = "Custom Panel Name";
...
```
