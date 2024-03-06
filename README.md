# DataGrid Icons Property

Since Stadium 6.8.3 we can use the column classes property to easily display icons in DataGrid columns. 



https://github.com/stadium-software/datagrid-icons-property/assets/2085324/7ccf47c7-a35e-48d9-9189-5deb6a58e697



## Version
1.0 initial release

# Setup

## Application Setup
1. Check the Enable Style Sheet checkbox in the application properties

## DataGrid Setup

1. Add a Connector, a DataGrid and populate the DataGrid with data as per usual (if you are not sure how, use [this](https://github.com/stadium-software/samples-database))

# Displaying an icon

Here are two ways to display an icon:

 [Option 1: Using the Iconify icons library](#option-1-using-the-iconify-icons-library)
 
 [Option 2: Using an image file](#option-2-using-an-image-file)

<hr>

## Option 1: Using the Iconify icons library

### Dependency

To display icons using the Icons library, the [Icons Module](https://github.com/stadium-software/icons) must be implemented in the application. There is no need to invoke the Icons script directly, but it must exist in the application. 

![](images/StadiumDesigner.png)

### Global Script Setup
1. Create a Global Script and call it "DataGridIcons"
2. Add the input parameter below to the Global Script
   1. HideHeaders
3. Drag a Javascript action into the script and paste the Javascript below unaltered into the action
```javascript
/* Stadium Script Version 1.0 - see https://github.com/stadium-software/datagrid-icons-property */
let hideheaders = ~.Parameters.Input.HideHeaders;
let hideh = true;
if (typeof hideheaders == "boolean" && hideheaders == false) { 
    hideh = false;
}
let dgs = document.querySelectorAll(".data-grid-container th.stadium-icon");
let attachHeadersCSS = () => { 
   let head = document.head;
   let style = document.createElement("style");
   style.innerHTML = `th.vh > * {
	position: absolute;
	width: 1px;
	height: 1px;
	margin: -1px;
	border: 0;
	padding: 0;
	white-space: nowrap;
	clip-path: inset(100%);
	clip: rect(0 0 0 0);
	overflow: hidden;
   }`;
   head.appendChild(style);
};
let initDGIcons = () => {
    observer.disconnect();
    let callIcons = true;
    for (let i = 0; i < dgs.length; i++) {
        if (hideh) dgs[i].classList.add("vh");
        let tbl = dgs[i].closest("table");
        let tds = tbl.querySelector("td.stadium-icon");
        if (!tds) {
            observer.observe(tbl, options);
            callIcons = false;
        }
    }
    if (callIcons) icons();
    attachHeadersCSS();
};
let options = {
        childList: true,
        subtree: true,
    },
    observer = new MutationObserver(initDGIcons);
let wait = async (milliseconds) => new Promise((resolve) => setTimeout(resolve, milliseconds));
let icons = async () => {
    try {
        await this.$globalScripts().Icons();
        return true;
    } catch (error) {
        wait(100).then(() => icons());
    }
};
initDGIcons();
```

### Page.Load Setup
1. Drag the "DataGridIcons" Global Script into the Page.Load Event Handler
2. Optionally, provide a value for script the Input Parameter
   1. HideHeaders (default is "true"): To show the DataGrid header for columns containing an icon, add "false"

### Datagrid Setup
1. Open the DataGrid "Columns" property
2. Select a column (usually a static column with a Click event)
3. Add the class 'stadium-icon' to the column "Classes" property
4. Find a symbol you wish to display (see [finding and icon](https://github.com/stadium-software/icons?tab=readme-ov-file#finding-an-icon))
5. Add the name of the symbol to the control classes property (e.g. 'material-symbols:edit' or 'material-symbols:delete')

*Example Classes*
```
stadium-icon material-symbols:edit
```

### Styling the icon
Additional classes can be added to the control classes property to manipulate the icon

1. Size
   1. The default icon size is 24px x 24px
   2. *icon-size-xx* allows you to define a custom icon size in pixels (e.g. icon-size-12 for 12px by 12px or icon-size-40 for 40px by 40px)
2. Color
   1. The default icon color is inherited by the page
   2. *icon-color-######* allows you to define a custom icon color in hex (e.g. icon-color-#FFFF00, icon-color-ccc or icon-color-red)

*Example Classes*
```
stadium-icon material-symbols:edit icon-size-24 icon-color-eeeeee
```

<hr>

## Option 2: Using an image file
1. Open the DataGrid "Columns" property
2. Select a column with a "Click" event (like "Edit" or "Delete") and locate the "Classes" property
3. Add a class of your choice to the selected column "Classes" property (e.g. edit-image)
4. Find a PNG, SVG or JPG icon file (e.g. use this [icons library](https://icones.js.org/collection/all) or just search on Google)
5. Drag the file into the "EmbeddedFiles" folder
6. Open the _Stylesheet_ in the Stadium Application Explorer
7. Paste the CSS below into the Stylesheet. **NOTE:** The CSS below assumes the image name is "edit.png"

```css
td.edit-image > *,
td.edit-image:hover > * {
    background-image: url('/src/assets/EmbeddedFiles/edit.png');
    background-repeat: no-repeat;
    background-size: 20px;
    background-position: center;
    height: 20px;
    width: 30px;
    font-size: 0;
}
```
