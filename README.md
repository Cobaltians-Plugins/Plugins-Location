#LocationPlugin

The Location plugin allows you to get the geolocation of the user.

## How to use

* Import the plugin to your project as explained [here](https://github.com/cobaltians/cobalt/wiki/Plugins-usage)
* Add the cobalt.location.js to your web JS folder
* Add an html `<link>` to the cobalt.location.js plugin script after the cobalt link in the `<head>` tag

## Basic usage

If you are a cowboy in a hurry, shoot this:

```
cobalt.location.start({
    onLocationChanged: function (location) {
        cobalt.log('Got location: ', location);
    }
});
```
## Functions

The following functions and properties are accessible _via_ the `cobalt.location` shortcut.

### Function `start (options)`

Start searching for the device geolocation. Once a correct location has been found, the plugin automatically stops. Takes one single object with the following properties as argument:

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `mode`  | String | `filter` | Can be `all` or `filter`:<br>- `all` returns every locations found<br>- `filter` returns only one location matching the following filters |
| `accuracy`  | Integer (meters) | `100` | Minimum accuracy of returned location |
| `timeout`  | Integer (milliseconds) | infinite | Stop searching for location after this timeout |
| `interval`  | Integer (milliseconds) | `500` | Minimum time interval between two location results in `all` mode |
| `age`  | Integer (milliseconds) | 120000 (2 minutes) | Maximum age of previous location (if any) |
| `onStatusChanged`  | Callback | Logging function | Shortcut to assign [`onLocationChanged`](#callback-onlocationchanged) |
| `onLocationChanged`  | Callback | Logging function | Shortcut to assign [`onStatusChanged`](#callback-onstatuschanged) |

### Function `stop ()`

Stop searching for location. Can be useful for the `all` mode or to cancel a long `filter` call.

### Callback `onLocationChanged`

Receives every location changes in `all` mode and just one in `filter` mode, taking one object as argument with the following properties:

| Name | Type | Description |
|------|------|-------------|
| `longitude` | Float | Longitude |
| `latitude` | Float | Latitude |
| `accuracy` | Integer | Location accuracy in meters |
| `timestamp` | Integer | Location timestamp in milliseconds |

### Enum `status`

This enum contains the different statuses that `onStatusChanged` can receive.

| Name | Description |
|------|-------------|
| `REFUSED` | The user has not enabled localization for this app |
| `DISABLED` | The user deactivated localization for this app after the localization started |
| `TIMEOUT` | No location matching the given filters were found |

### Callback `onStatusChanged`

Handles errors and timeout. It takes an object containing a `status` string that can be one of the above enum values.

In case of a `TIMEOUT` status, the most accurate location found is also present in a `location` property. Be careful with it, it can be quite far from your actual position.

### `cobalt.init` options

`onStatusChanged` and `onLocationChanged` can also be defined in `cobalt.init` like this:

```
cobalt.init({
    debug: true,
    plugins: {
        location: {
            onLocationChanged: function (location) { 
                cobalt.log('Location received: ', location);
            },
            onStatusChanged: function (data) { 
                cobalt.log('Status received: ', data.status);
            }

        }
    }
});
```

## Example

See the [catalog](https://github.com/Cobaltians-Samples/Samples-Catalog-Web/blob/master/plugins-location.html).

## Want more?

If you have any ideas or improvements to propose, please feel free to do so in the issue tracker!
