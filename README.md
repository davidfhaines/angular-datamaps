# Angular Datamaps
Provides an Angular directive to wrap https://github.com/markmarkoh/datamaps and easily build data maps in your Angular application.

 - Lightweight
 - Automatically updates on changes to bound data and options
 - No dependencies beside d3, topojson and datamaps
 - Documentation for available options can be found at https://github.com/markmarkoh/datamaps

![Datamap example](/usaMap.png?raw=true "USA Map Example")

## Install
Clone to your vendor directory
```sh
git clone git@github.com:dmachat/angular-datamaps.git
```

OR

Install with bower and save to your project's bower.json
```sh
bower install angular-datamaps --save
```

Add the module to your app dependencies and include it in your page.
```js
angular.module('app', [
  'datamaps'
]);
```

Load the datamaps and the two libraries datamaps depends on (d3 and topojson).
```html
<script src="d3.js"></script>
<script src="topojson.js"></script>
<script src="datamaps.all.js"></script>
<script src="angular-datamaps.js"></script>

<datamap
  options="map.options"
  data="map.data"
  colors="map.colors"
  type="{{ map.type }}"
  >
</datamap>
```

Add a map configuration object to your scope to bind to the directive
```js
$scope.map = {
  type: 'usa',
  data: [{
    values: [
      { "location": "USA", "value": 125 },
      { "location": "CAN", "value": 50 },
      { "location": "FRA", "value": 70 },
      { "location": "RUS", "value": 312 }
    ]
  }],
  colors: ['#666666', '#b9b9b9', '#fafafa'],
  options: {
    width: 1110,
    legendHeight: 60 // optionally set the padding for the legend
  }
}
```

### Geography click events ###
The datamaps click event can trigger a bound function with the clicked geography object. Just add your custom function to the `on-click` attribute, like this (notice there are no parenthesis):

```html
<datamap
  options="map.options"
  data="map.data"
  colors="map.colors"
  type="{{ map.type }}"
  on-click="updateActiveGeography"
  >
</datamap>
```

Then in your controller, that function gets the selected geography object as it's argument, like so:

```js
$scope.updateActiveGeography = function(geography) {
  $scope.stateName = geography.properties.name;
  $scope.stateCode = geography.id;
}
```

## Build it yourself!
angular-datamaps is built with grunt.

To run a simple connect server to see the directive in action or to develop
```sh
grunt dev
```

To run the tests
```sh
grunt test
```

or run in autotest mode

```sh
grunt autotest
```

And when you're done minify it
```sh
grunt build
```
