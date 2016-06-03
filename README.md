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

Start searching for the device geolocation. Takes one single object with the following properties as argument:

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| mode  | string | `filter` | Can be `all` or `filter`:<br>- `all` returns every locations found<br>- `filter` returns only one location matching the following filters |
| accuracy  | integer (meters) | `100` | Minimum accuracy of returned location |
| timeout  | integer (milliseconds) | infinite | Stop searching for location after this timeout |
| interval  | integer (milliseconds) | `500` | Time interval between two location results in `all` mode |
| age  | integer (milliseconds) | 120000 (2 minutes) | Maximum age of previous location (if any) |
| onStatusChanged  | callback | Logging function |  |
| onLocationChanged  | callback | Logging function | Called when a location has been found |

### Function `stop ()`

A function to stop searching for location. Can be useful for the `all` mode or to cancel a long `filter` call.

### Callback `onLocationChanged`

A callback that receive every location changes in `all` mode and just one in `filter` mode, taking one object as argument with the following properties :

```
{
    longitude: -3.4572026803687095,
    latitude: 48.75180676157803,
    accuracy: 180, // In meters
    timestamp: 1464947315568 // In milliseconds
}
```

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

`onStatusChanged` and `onLocationChanged` can also be defined in `cobalt.init` like this :

```
cobalt.init({
    debug: true,
    plugins: {
        location: {
            onLocationChanged: function (location) { 
                cobalt.log('location received :', location);
            },
            onSattusChanged: function (data) { 
                cobalt.log('location status changed :', data.status);
            }

        }
    }
});
```

## Want more?

If you have any ideas or improvements to propose, please feel free to do so in the issue tracker!
