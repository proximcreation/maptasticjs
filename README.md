maptastic
=========

Javascript/CSS projection mapping utility.  Put your internets on things!

### Usage:

When you include `maptastic.min.js` in your page, a new class named `Maptastic` is defined. The first step is to instantiate Maptastic, which can be done a couple of different ways depending on your needs. For most simple cases, this only requires a _single line of code_.

[SHOW ME THE DEMO!!!!](wefwf)

	<html>
	<head>
		<style>
			#so-simple{
				width:300px;
				height:300px;
				background:green;
			}
		</style>
	</head>
	<body>

		<div id="so-simple">This is pretty simple.</div>

		<script src="../build/maptastic.min.js"></script>
		<script>
			Maptastic("so-simple");
		</script>

	</body>
	</html>


### Constructor:

The constructor can be used in two different ways depending on how you would like to integrate with Maptastic.

#### Option 1 - Simple Setup

Specify a list of HTML elements, element IDs, or a mix of both. These elements will all be set up as Maptastic layers and will be configurable in edit mode.

	var element2 = document.getElementById("element-id2");
	
	Maptastic("element-id1", element2, ...);


#### Option 2 - Advanced Configuration

For more advanced useage, specify a configuration object. Available configuration properties are defined below.

	var configObject = {
		autoSave: false,
		autoLoad: false,
		onLayoutChange: myChangeHandler,
		layers: ["element-id1", "element-id2"]
	};
	Maptastic(configObject);

##### Configuration options

`layers` Array, default *empty*. Identical to Option 1 above, an array of IDs or HTML elements to be used as Maptastic layers.

`layoutChangeListener` function, default *null*. A function to be invoked whenever the layer layout is changed (if you want to implement your own save/load functionality).

`crosshairs` boolean, default *false*. Set the default crosshairs setting for edit mode, this can be toggled at run time with the `c` key.

`labels` boolean, default *true*. When in edit mode, show the element ID as an overlay.

`autoSave` boolean, default *true*. Control the automatic saving of layer positions into local storage.

`autoLoad` boolean, default *true*. Control the automatic loading of layer positions from local storage.


### Methods

In most cases, simply instantiating Maptastic with an element or two should be fine. However, if you are doing something more complicated, the Maptastic instance exposes several methods for controlling things at run time.

#### getLayout

Returns an array of layer descriptor objects that represent the current mapping configuration.  This can be helpful if you want to save the configuration to a remote database or something.

#### setLayout( _layoutData_ )

Sets the current mapping layout. The schema must match that returned from `getLayout` and is as follows:

	[
	  {
	    'id': 'some-element-id',
	    'targetPoints': [
	      [x1, y1],
	      [x2, y2],
	      [x3, y3],
	      [x4, y4]
	    ]
	  },
	  ...
	]


#### addLayer( _target_, _coordinates_ )

Add a new HTML element to be mapped.

`target` required. HTML Element or a string representing an element ID.

`coordinates` optional. An array of four two-dimensional arrays specifying the corner points. This is the same structure as the `targetPoints` array used in `getLayout` and `setLayout`


#### setConfigEnabled( _enabled_ )

Sets the current Configuration Mode state.

`enabled` boolean, required.