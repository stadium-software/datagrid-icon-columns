# DataGrid Icons

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
