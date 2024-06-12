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
4. Open the _Stylesheet_ in the Stadium Application Explorer
5. Paste the CSS below into the Stylesheet
6. Find an icon in this [icons library](https://icones.js.org/)
7. Copy the "Data URL" property (this copies a base64 encoded string that represents the icon)
[Data URL](images/data-url-location.png)
8. Replace **DATAURL** with the copied string (e.g. data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxZW0iIGhlaWdodD0iMWVtIiB2aWV3Qm94PSIwIDAgMjQgMjQiPjxwYXRoIGZpbGw9IiM2NjY2NjYiIGQ9Ik01IDE5aDEuNDI1TDE2LjIgOS4yMjVMMTQuNzc1IDcuOEw1IDE3LjU3NXptLTEgMnEtLjQyNSAwLS43MTItLjI4OFQzIDIwdi0yLjQyNXEwLS40LjE1LS43NjN0LjQyNS0uNjM3TDE2LjIgMy41NzVxLjMtLjI3NS42NjMtLjQyNXQuNzYyLS4xNXQuNzc1LjE1dC42NS40NUwyMC40MjUgNXEuMy4yNzUuNDM3LjY1VDIxIDYuNHEwIC40LS4xMzguNzYzdC0uNDM3LjY2MmwtMTIuNiAxMi42cS0uMjc1LjI3NS0uNjM4LjQyNXQtLjc2Mi4xNXpNMTkgNi40TDE3LjYgNXptLTMuNTI1IDIuMTI1bC0uNy0uNzI1TDE2LjIgOS4yMjV6Ii8+PC9zdmc+)

```css
td.edit-image > *,
td.edit-image:hover > * {
    background-image: url(DATAURL);
    background-repeat: no-repeat;
    background-size: 20px;
    background-position: center;
    height: 20px;
    width: 30px;
    font-size: 0;
}
```
