#LocationPlugin

Location plugin allows you to get the geolocation of the user.


## How to use

* import the plugin to your project as explained [here](https://github.com/cobaltians/cobalt/wiki/Plugins-usage)
* Add the cobalt.location.js to your web JS folder
* Add an html link to the cobalt.location.js plugin script after the cobalt link in the HEAD tag

## Shortest usage

If you are a cowboy in a hurry, shoot this :

```
cobalt.location.start({
	mode : 'filter',
	onLocationChanged:function(location){
		cobalt.log('Got location', location);
	}
});
```

## location.start

start takes one single object as argument. here are the available property of this object.

| property | type | default value | description |
| -------- | ---- | ------------- | ----------- |
| mode  | string | **this property is mandatory** | Can be `all` or `filter`. <br> - The `all` mode returns every locations found<br> - The `filter` mode returns only one location |
| accuracy  | number (metters) | 100 | Minimum accuracy of returned locations |
| timeout  | number (ms) | undefined | Stop searching location after this timeout |
| frenquency  | number (ms) | 500 | Number of ms between two location results in `all` mode |
| timestamp  | number (ms) | 12000 (=2mins) | max age of previous location (if any) |
| onStatusChanged  | function |  | see [location.onSattusChanged](#location.onSattusChanged) bellow |
| onLocationChanged  | function |  | see [location.onLocationChanged](#location.onLocationChanged) bellow |

## location.stop

Stop searching location now. For the `all` mode or to cancel a long `filter` call.

## location.onSattusChanged

A callback to handle errors and timeout. It receive a status string that can be :

* `disabled` if the user disabled location for this app.
* `refused` if the user refused to enable location for this app.
* `timeout` if the location plugin hits the timeout defined.

## location.onLocationChanged

A callback that receive every location changes in `all` mode and just one in `filter` mode.

It receive one location parameter. Here is an example value :

```
{
    lng : -3.4572026803687095,
    lat : 48.75180676157803,
    accuracy : 180,
    timestamp : 1449759043
}
```

`accuracy` and `timestamp` are only returned in `all` mode.


## cobalt.init options

`location.onSattusChanged` and `location.onLocationChanged` can also be defined in cobalt.init like this :

```
cobalt.init({
    debug : true,
    plugins : {
        location : {
            onLocationChanged : function(location){ 
                cobalt.log('location received :', location)
            },
            onSattusChanged : function(status){ 
                cobalt.log('location status changed :', status)
            }

        }
    }
})
```

##Platforms

**warning** this is not coded yet on iOS !


##Planned features

Next features are:

 * please suggest in the issue tracker or pull request your own changes!
