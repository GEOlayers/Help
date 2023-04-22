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

Find an overview of the functions the API exposes:

#### geolayers3.importProject(file[, isLabelTemplateProject])
Import a project to your current one. GEOlayers will sort everything into its project structure, take care of unique comp names and update expressions accordingly. 

Arguments:

  file: A File object referencing an .aep or .aet file.
  isLabelTemplateProject: Boolean, set to true if the project to import only contains Label Templates.

#### geolayers3.finalize(comps, callback[, options])
Use it to finalize Mapcomps. 
Arguments:
comps: Either one or an array of Mapcomp names, Mapcomps or comps that contain Mapcomps, or undefined to finalize all Mapcomps in the project.
callback: A function (error, mapcomps) that is called async when all finalizations are done.
options: An options object with the following possible boolean properties: "onlyCurrentFrame", "previewQuality", "onlyWorkArea" and "purgeImageryCache".
Note that this is an async function. This means any scripting that has to be done after the finalization needs to be placed inside the callback function. It takes an error as the first and the finalized compositions as the second argument and is called after all finalizations are done.


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
