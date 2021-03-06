# cesium-navigation
This is a Cesium plugin that adds to the Cesium map a user friendly compass, navigator (zoom in/out), and
distance scale graphical user interface.

**Why did you build it?**

First of all the Cesiumjs sdk does not includes a compass, navigator (zoom in/out), and distance scale. You can use the mouse to navigate on the map, but this navigation plugin  offers more navigation control and capabilities to the user. Some of the capabilities are: reset the compass to point to north, reset the orbit, and 
reset the view to a default bound.

**How did you build it?**

This plugin is based on the excellent compass, navigator (zoom in/out), and distance scale from the terriajs open source library (https://github.com/TerriaJS). The navigation UI from terriajs can not be used out of the box in Cesium because Cesium uses CommonJS modules with RequireJS, and the terriajs uses commonjs and Browserify, so you can't just copy the source files into Cesium and build.  My work consisted on adapting the code to work within Cesium as a plugin as follows:

- extracted the minimum required modules from terriajs.
- Converted all the modules from Browserify to requirejs.
- Use gulpjs to compile and minify the less files, bundle and minify all the modules and open source dependencies 
  into just one file. As part of the build process I decided to replace requirejs with almondjs to reduce the footprint of the AMD loader used in the plugin. The almondjs library is also bundle inside the plugin to make the plugin as easy as plug and play within Cesium.

**How to use it?**

- add the cesium-navigation folder from the distribution (dist) folder into your Cesium map application. Or download the plugin from gitHub and build a release version of the plugin as follows:

		gulp release-unminified --> for the unminified plugin for debugging purposes.
		gulp default --> for the minified plugin (recommended)

- Add the cesium-navigation/cesium-navigation.js script  to your html file.
- Add the style	as follows:

 		@import url(<path>/cesium-navigation/cesium-navigation.css);


- Inside the body of your page add the following:

		var viewer = new Cesium.Viewer('cesiumContainer');
		navigationInitialization('cesiumContainer', viewer);
		
		if using the CesiumWidget:
		
		var widget = new Cesium.CesiumWidget('cesiumContainer',
			{
     				imageryProvider: new Cesium.TileMapServiceImageryProvider({
                            		url:: 'javascript/Cesium/Assets/Texture/NaturalEarthII'
             		})
		});
		navigationInitialization('cesiumContainer', widget );

The navigationInitialization function initializes the navigation plugin within the Cesium viewer. 
This function also assigns the instantiated plugin navigation object to the viewer (viewer.navigation).

- To destroy the navigation object and release the resources later on, use the following

		viewer.navigation.destroy();
		viewer.navigation = undefined;
		
		if using the CesiumWidget:
		
		widget.navigation.destroy();
		widget.navigation = undefined;


**Is there a demo using the plugin ?**

This is the demo:

(http://alberto-acevedo.github.io/cesium-navigation/)

- The compass, navigator, and distance scale will appear on the right side of te map.
-  This plugin was successfully tested on Cesiumjs version 1.15. It works great with Cesium in 3D mode. Recently Larcius (https://github.com/Larcius) made a lot of improvements and fixed some issues in Columbus and 2D modes.

**What about the license?**
 - The plugin is 100% based on open source libraries. The same license that applies to Cesiumjs and terriajs applies also to this plugin. Feel free to use it,  modify it, and improve it.
