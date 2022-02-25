# gee-blend
#### _Jesse Anderson_

## About
_gee-blend_ is a code module for using blended visualizations in [Google Earth Engine](https://earthengine.google.com). It can be loaded in the playground by clicking [here](https://code.earthengine.google.com/?accept_repo=users/jja/public), which will add the repository containing the code to the _Reader_ section of the _Scripts_ tab, under `users/jja/public`. The script _blend_demo.js_ illustrates some of its basic functionality.

## Using the Module

You can load the module in your code by running

```javascript
var blend = require('users/jja/public:blend.js');
```

Blend functions can be applied using the following pattern: `blend.<function>(top_image, bottom_image);`
Where `<function>` is one of the following:
- addition
- burn
- darken
- difference
- dodge
- hard_light
- lighten
- multiply
- normal
- overlay
- screen
- subtract

`

Here is an example blend operation and output.

Code:
```javascript
// Load the module
var blend = require('users/jja/public:blend.js');

// Load and visualize a digital elevation model
var dem = ee.Image("CGIAR/SRTM90_V4");
var dem_rgb = dem.visualize({
  min:100, 
  max:6000, 
  palette: ['#000004', '#50127b', '#b63679', '#fc8761', '#fdfd65'],
  forceRgbOutput:true
});

// Derive and visualize a slope image
var slope_rgb = ee.Terrain.slope(dem).visualize({
  min:0, 
  max:90, 
  palette: ['#000000', '#ffffff'],
  forceRgbOutput:true
});

// Use the `difference` blend function and add to the map
Map.addLayer(blend.difference(dem_rgb, slope_rgb), {min:-41, max:163});

// Zoom to an interesting location
Map.setCenter(71.2, 36, 9);
```
Image:
![blend_ex_1](https://user-images.githubusercontent.com/1250693/155811215-dbba64db-30ab-4fcf-9472-be7425a99e54.png)



## License

The blend code is licensed under the terms of the [MIT license](https://opensource.org/licenses/MIT).
