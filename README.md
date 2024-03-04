# DataGrid Icons Property

Since Stadium 6.8.3 we can use the column classes property to easily display icons in DataGrid columns. 

## Version
1.0 initial release

# Setup

## Application Setup
1. Check the Enable Style Sheet checkbox in the application properties

## DataGrid Setup

1. Add a Connector, a DataGrid and populate the DataGrid with data as per usual (if you are not sure how, use [this](https://github.com/stadium-software/samples-database))
2. Open the DataGrid "Columns" property
3. Select a column with a "Click" event (like "Edit" or "Delete") and locate the "Classes" property
4. Add a class of your choice to the column (e.g. edit-image)

## Displaying the icon as a background image

1. Find an icon file
2. Drag it into the "EmbeddedFiles" folder
3. Open the _Stylesheet_ in the Stadium Application Explorer
4. Paste the CSS below into the Stylesheet. **NOTE:** The CSS below assumes the image name is "edit.png"

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
