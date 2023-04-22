# GEOLayers Help
# Basic

GEOlayers is your new best friend when you want to design and animate maps. It hooks you up with up-to-date geospatial data and satellite imagery. It lets you design complex map styles with a few clicks and animate them in 3D space. Watch this tutorial to get started. Learn how to create Mapcomps, change styles, animate, and finalize them.

### Mapcomps

![mapcomp](https://user-images.githubusercontent.com/19971466/233547961-62f27e76-a9e3-4a64-815d-2f6af515c708.png)

Mapcomps are Compositions filled with map imagery and/or geographical labels.
They are the basic building block of each GEOlayers project.

To start a project you need to create a Mapcomp. Do this by creating a new project from the projects window or click the little arrow top left in the main window and hit + Add Mapcomp.

There are two steps to add a new Mapcomp:

1. Composition options and location
Choose a name, pixel size, duration, and framerate. These values are set from the currently selected composition. Don't forget to navigate the preview map to the location you're interested in. You can also use the search bar to jump to a place. Once you did this hit Next
2. Map Style
Now select a basic style for your map. You can select imagery presets from the section below the preview map, choose color presets, or change individual colors. The Mapcomp can be styled more detailed once it is created, so hit Create for now!
Now you can see the actual Mapcomp has beed created in the currently selected composition. Above it you can see the Mapcomps anchor layer. This is a helper layer that matches the Mapcomp's view animation and can be used to parent layers.

If you don't want to start from scratch you can also choose a sample project to start from. Find the projects panel in the context- or flyout menu of the GEOlayers panel.

Whenever you open a project that already contains Mapcomps you can see and select them clicking  top left in the main window. This will open the Mapcomp list.

As you hover over a Mapcomp the following buttons appear:

# Scripting API
There is an extend script API that you can use to automate tasks with GEOlayers. Feel free to get in touch and tell us what you need to create automated workflows. In general, the GEOlayers panel needs to be open when you want to call any function of the API.

Download Scripting Examples [here](https://geolayers3-live.firebaseapp.com/scriptingApiExamples.zip)

Find an overview of the functions the API exposes:

### geolayers3.importProject(file[, isLabelTemplateProject])
Import a project to your current one. GEOlayers will sort everything into its project structure, take care of unique comp names and update expressions accordingly. 
Arguments:
  - **file:** A File object referencing an .aep or .aet file.
  - **isLabelTemplateProject:** Boolean, set to true if the project to import only contains Label Templates.

### geolayers3.finalize(comps, callback[, options])
Use it to finalize Mapcomps. 
Arguments:
- **comps:** Either one or an array of Mapcomp names, Mapcomps or comps that contain Mapcomps, or undefined to finalize all Mapcomps in the project.
- **callback:** A function (error, mapcomps) that is called async when all finalizations are done.
- **options:** An options object with the following possible boolean properties: "onlyCurrentFrame", "previewQuality", "onlyWorkArea" and "purgeImageryCache".

Note that this is an async function. This means any scripting that has to be done after the finalization needs to be placed inside the callback function. It takes an error as the first and the finalized compositions as the second argument and is called after all finalizations are done.

### geolayers3.duplicate(comp[, options])
Use it to duplicate Mapcomps or comps that contain Mapcomps. This method also updates all related expressions. 
**Arguments:**
- **comp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp
- **options:** An options object. Use it for naming the duplicates. If you're duplicating a Mapcomp use the property "newName". If you duplicate a containing comp use "newContainingCompName"

This function returns the duplicate comp or undefined if anything goes wrong.

### geolayers3.setViewAtTime(comp, view[, forceKeyframe[, time]])
Use it to set or animate views of Mapcomps.

**Arguments:**
- **comp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp
- **view:** An object with the following float properties: "latitude", "longitude", "zoom", "bearing" and "pitch".
- **forceKeyframe:** Set this to true to set a keyframe even if the property is not keyframed yet.
- **time:** The time in the containing comp to set the value. If it is undefined it takes the current time.

This function returns the applied view object or undefined if anything goes wrong.

### geolayers3.fitViewAtTime(comp, bbox[, forceKeyframe[, time]])
Use it to set or animate views of Mapcomps by a bounding box. 

**Arguments:**
- **comp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp
- **bbox:** A geojson bounding box Array [LongitudeMin, LatitudeMin, LongitudeMax, LatitudeMax] (WGS 84)
- **forceKeyframe:** Set this to true to set a keyframe even if the property is not keyframed yet.
- **time:** The time in the containing comp to set the value. If it is undefined it takes the current time.

This function returns the applied view object or undefined if anything goes wrong.

### geolayers3.removeMapcompControlKeys(comp)
Removes all keyframes from the Latitude, Longitude, Zoom, Bearing and Pitch controls of the specified Mapcomp. 

**Arguments:**
- **comp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp

### geolayers3.getMapcomps()
Returns all mapcomps of the project.

### geolayers3.getMapcompAnchor(mapcomp)
Returns the mapcomp's anchor layer in their containing comp. 

**Arguments:**
- **mapcomp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp

### geolayers3.getLabelTemplateComps()
Returns the projects Label Template Compostioions or an empty Array.

### geolayers3.addLabel(comp, labelTemplateComp, labelData)
Use it to add Labels to Mapcomps.

**Arguments:**
- **comp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp
- **labelTemplateComp:** A composition, label template name or an integer representing the number of the label template in the project.
- **labelData:** An object with the following required float properties: "latitude" or "lat" and "longitude" or "lon" plus the string properties the label template requires like "name" ect.

This function returns the label layer or undefined if anything goes wrong.

### geolayers3.updateLabelData(labelLayer, newLabelData)

Use it to update data in already created Template Labels. 

**Arguments:**
- **labelLayer:** A Label Layer
- **newLabelData:** An object with the string properties the label template requires like "name" ect.

This function returns the label layer or undefined if anything goes wrong.

### geolayers3.getLayersGeoPosition(layer)
Use it to get longitude and latitude of a layer in relation to a Mapcomp. 
**Arguments:**
- **layer:** A layer in a mapcomps containing comp

This function returns an array [longitude, latitude] or undefined if anything goes wrong.

### geolayers3.fetchText(url, callback[, initObject])
Hit an url and get back the response as text. 
**Arguments:**
- **url:** The url you want to fetch.
- **callback:** A function(error, data) that is called async when the response has been processed.
- **initObject:** Please search the fetch API docs for the init object.

Note that this is an async function. Means that any scripting that has to be done after the request needs to be placed inside the callback function. It takes an error as the first and the responded data as the second argument and is called after the response has been processed.

### geolayers3.fetchJson(url, callback[, initObject])
A quick way to hit json apis.
**Arguments:**
**url:** The url you want to fetch.
**callback:** A function(error, data) that is called async when the response has been processed.
**initObject:** Please search the fetch API docs for the init object.
Note that this is an async function. Means that any scripting that has to be done after the request needs to be placed inside the callback function. It takes an error as the first and the responded data as the second argument and is called after the response has been processed.

### geolayers3.geocode(searchString, callback[, options])
A quick way to geocode a string. Pretty much the same as if you would type it into the searchbar. 

**Arguments:**
- **searchString:** The search term or address you want to geocode.
- **callback:** A function(error, features) that is called async when the response has been processed.
- **options:** An options object with the following possible ISO639 string property: "language". By default the selected Mapcomp's setting will be used.

Note that this is an async function. Means that any scripting that has to be done after the request needs to be placed inside the callback function. It takes an error as the first and an array of geojson features as the second argument and is called after the response has been processed. This function uses OpenStreetMap Nominatim search engine. You shouldn't bulk geocode placenames. The geolayers scripting api will queue multiple requests at the same time according to the Nominatim usage policy.

### geolayers3.watch(fileOrFolder, callback[, options])
Watches a file or folder for changes. If a file or folder is allready being watched it will be canceled. 

**Arguments:**
- **fileOrFolder:** A File or Folder object to watch.
- **callback:** A function(file) or function(changedFilesInFolder, allFilesInFolder) that is called each time the file or a file in the folder changes. If the scripting api is busy finalizing(or any other async method) the function will be called after the next interval.
- **options:** An options object with the following possible integer property: "interval" which is the intervall between the checks in ms defaults to 10000.

### geolayers3.watchCsv(csvFile, callback[, options])
Watches a file or folder for changes. If a file or folder is allready being watched it will be canceled. 

**Arguments:**
- **csvFile:** A File object referencing a .csv, .tsv or .txt file to watch.
- **callback:** A function(changedRows, allRows) that is called each time the csv file changes. If the scripting api is busy finalizing(or any other async method) the function will be called after the next interval.
- **options:** An options object with the following possible properties: "interval" integer which is the intervall between the checks in ms, defaults to 10000. "delimiter" string used to split values of the file, defaults to ",".

### geolayers3.unwatch()
Stops the current watch task.

### geolayers3.addToBrowser(addObj, [callback[, options]])
Adds fretures to the browser even from a file, a geocoding request, an overpass api query or a geojson object. 

**Arguments:**
- **addObj:** Can be one of the following objects:
  - ExtendScript File object referencing a geospatial file
  - Url to a geospatial file. The url should contain the file extension.

```
geojson object
{
type: "geocode",
query: "Term to geocode"
}
{
type: "overpass",
query: "Overpass query"
}
{
type: "osm",
id: "OpenStreetMap Id (something like node1234 or way4321 or rel1243)"
}
{
type: "geojsonurl",
url: "Url to geojson"
}
```

- **callback:** A function(error, data) that is called after the data has been imported to the browser.
- **options:** An options object with the following possible properties:
  - **returnData boolean:** Set to true to return the data in the callback, defaults to false since this can be very slow for larger features.
  - **pointGeometries boolean:** Return the Feature as a Point representation, which is way faster for complex Geometries.
  - **normalizeToFeatureArray boolean:** Return an Array of Features instead of possible nested Feature Collections.
  - **name string:** A name for the root feature or feature collection that is imported.
  - **namingProp string:** The property that should be used to name all imported features.

### geolayers3.clearBrowser([callback])
Removes all features but the favorites from the browser. 

**Arguments:**
- **callback:** A function(error, data) that is called after the browser has been cleared.

### geolayers3.removeBrowserSelection([callback])
Removes selected features from the browser. 

**Arguments:**
- **callback:** A function(error, data) that is called after features have been removed.

### geolayers3.getBrowserSelection([callback[, options]])
Get features that are selected in the browser. 

**Arguments:**
- **callback:** A function(error, data) with an Array of selected features as data.
- **options:** An options object with the following possible properties:
- **fullGeometry boolean:** Set to true to return the features full geometry instead of just a point. This can be very slow for large geometries.

### geolayers3.drawBrowserSelection(comp, [callback[, options]])
Draws features which are selected in the browser of the GEOlayers 3 panel to a Mapcomp. 

**Arguments:**
- **comp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp
- **callback:** A function(error, data) that is called after the data has been imported to the browser.
- **options:** An options object with the following possible properties:
  - **shapeLayerStyle:** an index number, name or shape layer style object
  - **drawInsideMapcomp:** defaults to **false**
  - **autoStrokeWidth:** defaults to **false**
  - **simplify:** defaults to **true**
  - **simplyfyByZoomRange:** defaults to **false**
  - **simplificationZoomOffset:** defaults to **0**
  - **useTopoSimplificationIfPossible:** defaults to **false**
  - **individualLayers:** defaults to **false**
  - **autoChangeRenderer:** defaults to **false**
  - **addTrimPaths:** defaults to **false**
  - **duration:** defaults to **10**
  - **dateBorderCopy:** defaults to **false**
  - **dashThreshold:** defaults to **1**
  - **absoluteZScale:** defaults to **false**
  - **castsShadows:** defaults to **false**
  - **acceptsShadows:** defaults to **false**
  - **lockLayerTransforms:** defaults to **false**

### geolayers3.draw(comp, addObj, [callback[, options]])
Draws features to a Mapcomp. Features are specified with an addObj like in the .addToBrowser() method. 
**Arguments:**
- **comp:** A Mapcomp name, Mapcomp or comp that contains a Mapcomp
- **addObj:** Can be one of the following objects:

ExtendScript File object referencing a geospatial file
Url to a geospatial file. The url should contain the file extension.
```
geojson object
{
type: "geocode",
query: "Term to geocode"
}
{
type: "overpass",
query: "Overpass query"
}
{
type: "osm",
id: "OpenStreetMap Id (something like node1234 or way4321 or rel1243)"
}
{
type: "geojsonurl",
url: "Url to geojson"
}
```
- **callback:** A function(error, data) that is called after the data has been imported to the browser.
- **options:** An options object with the following possible properties:
  - **shapeLayerStyle:** an index number, name or shape layer style object
  - **drawInsideMapcomp:** defaults to **false**
  - **autoStrokeWidth:** defaults to **false**
  - **simplify:** defaults to **true**
  - **simplyfyByZoomRange:** defaults to **false**
  - **simplificationZoomOffset:** defaults to **0**
  - **useTopoSimplificationIfPossible:** defaults to **false**
  - **individualLayers:** defaults to **false**
  - **autoChangeRenderer:** defaults to **false**
  - **addTrimPaths:** defaults to **false**
  - **duration:** defaults to **10**
  - **dateBorderCopy:** defaults to **false**
  - **dashThreshold:** defaults to **1**
  - **absoluteZScale:** defaults to **false**
  - **castsShadows:** defaults to **false**
  - **acceptsShadows:** defaults to **false**
  - **lockLayerTransforms:** defaults to **false**

### geolayers3.filesInDir(folder[, filterRegEx[, includeSubDirectories]])
Returns File objects of all Files in the given folder matching the filter regular expression. It can also include sub directories. 

**Arguments:**
- **folder:** Extend Script Folder Object.
- **filterRegEx:** Regular expression to test on the file name.
- **includeSubDirectories:** Boolean, set to true to include files from sub directories.
Returns a string.

### geolayers3.readFile(file[, encoding])**
Reads the contents of a file. 

**Arguments:**
- **file:** Extend Script File Object or filename string.
- **encoding:** String, defaults to UTF8. For details check out the Extend Script Tools Guide
Returns a string.

### geolayers3.readFileCsv(file[, encoding])
Reads the contents of a .csv or .tsv file. 

**Arguments:**
- **file:** Extend Script File Object or filename string.
- **encoding:** String, defaults to UTF8. For details check out the Extend Script Tools Guide
Returns an Array of rows where each row is an Array of columns.

### geolayers3.readFileJson(file[, encoding])
Reads the contents .json file. 

**Arguments:**
- **file:** Extend Script File Object or filename string.
- **encoding:** String, defaults to UTF8. For details check out the Extend Script Tools Guide
Returns a JavaScript Object.

### geolayers3.writeFile(file, content[, encoding])
Writes a file to disk. 

**Arguments:**
- **file:** Extend Script File Object or filename string.
- **content:** String to write to the file.
- **encoding:** String, defaults to UTF8. For details check out the Extend Script Tools Guide

### geolayers3.userFolder()
Returns a Folder Object referencing the GEOlayers User Folder.

### geolayers3.userFile(fileName)
Returns a File Object referencing a File with the fileName inside the GEOlyers User Folder. 

**Arguments:**
- **fileName:** File 'basename.extension' string.

### geolayers3.modalEditObject(obj, callback[, options])
Use the GEOlayers 3 UI to edit properties of a simple flat javascript object. It can handle strings, numbers and booleans. 

**Arguments:**
- **obj:** A simple flat object to edit like: {name: "New York", id: 12, selected: true}
- **callback:** A function(error, editedObj) that is called after the user applied his edits or canceled.
- **options:** An options object with the following possible string properties: "title", "message" Both to be displayed in the UI.

### geolayers3.modalActions(actions, callback[, options])
Use the GEOlayers 3 UI to edit properties of a simple flat javascript object. It can handle strings, numbers and booleans. 

**Arguments:**
- **actions:** An array of strings to be displayed as buttons
- **callback:** A function(error, actionsIndex) that is called after the user clicked one of your action buttons or canceled. The index of the action in the actions array or undefined in case he canceled will be returned as actionsIndex.
- **options:** An options object with the following possible string properties: "title", "message" Both to be displayed in the UI.

### geolayers3.githubBrowser([options])
Show a panel in which you can browse GitHub Repos and perform actions like importing files from it. 

**Arguments:**
- **options:** An object that can have the following properties and methods:
  - **title (String)** panel title
  - **defaultUser (String)** initial GitHub username
  - **defaultRepo (String)** initial GitHub repository name
  - **fixedRepo (Boolean)** allow the user to change github user and repo or not
  - **flatten (Boolean)** initial Flatten folders value
  - **filterText (String)** initial text for the browsers filter bar
  - **actionBtnText (String)** text to display the button that triggers the action callback, defaults to "Import to GEOlayers"
  - **actionFilter (Function)** filter function(item) that should return true if the item is suitable for the action callback, defaults to accepting geojson files
  - **action (Function) function(item, url)** to be performed as the user clicks the action button, defaults to importing it the Feature Browser

Download Scripting Examples [here](https://geolayers3-live.firebaseapp.com/scriptingApiExamples.zip)

---------------------------------------------------------------------------------------------------------------------------------------------------------

# MapTiler Data
Some functions of GEOlayers are only possible because we partnered with MapTiler as a data provider.

This partnership allows us to provide these features:

Stylized Mapcomp Imagery (The imagery styles with the MapTiler icon)
Find Features by clicking the preview map
Mapcomp labels in different languages
Watermask Mapcomps from the toolbar
Feature import for the current view to the browser
Drawing 3D buildings from the toolbar
After the free trial to check it out you'll need a Flex plan on MapTiler Cloud to enable these features.

You can of course use GEOlayers without it.

# Disclaimer
The terms of use of the map service providers apply. Content must be attributed unless otherwise agreed with the map service provider.

GEOlayers cannot ensure that every tileserver, geocoding-service, or other external geodata source work properly all the time. Certain functions will not work if remote servers are down, which are out of our control.

The creators of GEOlayers are not responsible for the topicality, correctness, completeness, or quality of the information provided or acquired with this software from the aforementioned exernal map service providers. GEOlayers cannot be held liable for damages caused by the use of any information provided, including any kind of information which is incomplete or incorrect. All offers are unbinding and without obligation.

The creators of GEOlayers do not claim any ownership or license for the images and data you acquire with this software from any map service provider.
