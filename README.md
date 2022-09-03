# English | [简体中文](./README.zh.md)

# Introduction

Plugins for improving the availability of Cesium.

# Installation

```
npm i cesium-plugins
```

# Overview

- [PositionPicker](https://github.com/syzdev/cesium-plugins#positionpicker)：Plugin for left mouse click to pick up longitude, latitude, and height.

- [Cesium3DTilesLoader](https://github.com/syzdev/cesium-plugins#cesium3dtilesloader)：Plugin for loading and configuring 3DTiles.

- [Tooltip](https://github.com/syzdev/cesium-plugins#Tooltip)：Plugin for creating tooltip that follow mouse movement.

# API

## PositionPicker

Plugin for left mouse click to pick up longitude, latitude, and height.

Live Demo: [PositionPicker](https://syzdev.cn/cesium-plugins/example/PositionPicker.html) (View the output in the browser console.)

### `constructor(Cesium, viewer)`

Constructor, used to initialize the instance object of `PositionPicker`.

| Name     | Type     | Default | Description                         |
| -------- | -------- | ------- | ----------------------------------- |
| `Cesium` | `Object` |         | Cesium global object                |
| `viewer` | `Object` |         | Initialize `viewer` of Cesium scene |

```javascript
import { PositionPicker } from 'cesium-plugins'
const picker = new PositionPicker(Cesium, viewer)
```

### `pick(callback, verbose)`

The core function is used to pick up longitude, latitude and height by clicking the left mouse button. The obtained longitude, latitude, and height can be obtained in the `callback` function.

| Name       | Type       | Default | Description                                                              |
| ---------- | ---------- | ------- | --------------------------------------------------------------- |
| `callback` | `Function` |         | Callback function for obtaining longitude, latitude and height  |
| `verbose`  | `Boolean`  | `true`  | Whether to output longitude, latitude and height on the console |

```javascript
picker.pick(({ lon, lat, hgt }) => {
  console.log(lon, lat, hgt)
}, true)
```

### `destroy()`

Used to destroy the `PositionPicker` instance object.

```javascript
picker.destroy()
```

## Cesium3DTilesLoader

Plugin for loading and configuring 3DTiles.

Live Demo: [Cesium3DTilesLoader](https://syzdev.cn/cesium-plugins/example/Cesium3DTilesLoader.html)

### `constructor(Cesium, viewer)`

Constructor, used to initialize the instance object of `Cesium3DTilesLoader`.

| Name     | Type     | Default | Description                         |
| -------- | -------- | ------- | ----------------------------------- |
| `Cesium` | `Object` |         | Cesium global object                |
| `viewer` | `Object` |         | Initialize `viewer` of Cesium scene |

```javascript
import { Cesium3DTilesLoader } from 'cesium-plugins'
const loader = new Cesium3DTilesLoader(Cesium, viewer)
```

### `load(url, posOpts, loadOpts): Cesium3DTileset `

The core function is used to load and configure 3DTiles.

| Name       | Type     | Default         | Description                                                                                                           |
| ---------- | -------- | --------------- | --------------------------------------------------------------------------------------------------------------------- |
| `url`      | `String` |                 | The resource path to `tileset.json`                                                                                   |
| `posOpts`  | `Object` | (See below)     | Load the position, rotation, and scale parameters for 3DTiles                                                         |
| `loadOpts` | `Object` | (See below) | Load the configuration of 3DTiles, which is consistent with the `option` configuration of the `Cesium3DTileset` class |

This function will return an instance object of `Cesium3DTileset`.

The parameter list and default configuration of `posOpts` are as follows:

```javascript
{
  lon: 116.391311, // Longitude (in decimal)
  lat: 39.90616, // Latitude (in decimal)
  hgt: 0, // Height (in meters)
  rx: 0, // X axis (longitude) direction rotation Angle (in degrees)
  ry: 0, // Y axis (latitude) direction rotation Angle (in degree)
  rz: 0, // Z axis (height) direction rotation Angle (in degree)
  scale: 1, // Scale of the 3DTiles
},
```

`loadOpts` is consistent with the `option` configuration of the `Cesium3DTileset` class，See: [Cesium3DTileset - Cesium Documentation](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileset.html?classFilter=Cesium3DTileset#Cesium3DTileset)，For example, you can add the following configuration:

```javascript
{
  maximumScreenSpaceError: 256,
  maximumMemoryUsage: 5120,
  immediatelyLoadDesiredLevelOfDetail: true,
}
```

Complete example:

```javascript
const url = 'https://syzdev.cn/cesium-docs-demo/3dtiles/tlfs/tileset.json'
const posOpts = {
  lon: 114.296,
  lat: 30.546,
  hgt: 0,
  scale: 1
}
const loadOpts = {
  maximumScreenSpaceError: 256,
  maximumMemoryUsage: 5120,
  immediatelyLoadDesiredLevelOfDetail: true,
}
const tileset = loader.load(url, posOpts, loadOpts)
```

### `locate()`

Used to position the perspective on the loaded 3DTiles.

```javascript
loader.locate()
```

### `destroy()`

Used to destroy the `Cesium3DTilesLoader` instance object.

```javascript
loader.destroy()
```

## Tooltip

Plugin for creating tooltip that follow mouse movement.

Live Demo: [Tooltip](https://syzdev.cn/cesium-plugins/example/Tooltip.html)

### `constructor(Cesium, viewer, msg, tooltipOpts)`

Constructor, used to initialize the instance object of `Tooltip`.

| Name          | Type     | Default     | Description                                                     |
| ------------- | -------- | ----------- | --------------------------------------------------------------- |
| `Cesium`      | `Object` |             | Cesium global object                                            |
| `viewer`      | `Object` |             | Initialize `viewer` of Cesium scene                             |
| `msg`         | `String` |             | Contents displayed in tooltip                                   |
| `tooltipOpts` | `Object` | (See below) | Configuration related to tooltip, such as location, style, etc. |

```javascript
import { Tooltip } from 'cesium-plugins'
const tooltip = new Tooltip(Cesium, viewer, 'cesium-plugins', tooltipOpts)
```

The parameter list and default configuration of `tooltipOpts` are as follows:

```javascript
{
  // Offset of Tooltip from mouse (in px)
  offset: {
    left: 30,
    top: 50,
  },
  // The style of the Tooltip container
  containerStyle: {
    display: 'block',
    position: 'absolute',
    maxWidth: '150px',
    minWidth: '100px',
    borderRadius: '4px',
    background: '#757575',
    color: '#fafafa',
    zIndex: '999',
  },
  // The style of the Tooltip content
  innerStyle: {
    padding: '5px 8px',
    fontSize: '10px',
    fontWeight: '400',
  },
  // Whether to display Tooltip only when mouse is on Earth
  isShowOnlyOnEarth: true,
}
```

Complete example:

```javascript
const tooltipOpts = {
  offset: {
    top: 40,
    left: 20,
  },
  containerStyle: {
    maxWidth: '250px',
    color: '#fff',
    background: 'rgb(109, 171, 228)'
  },
  innerStyle: {
    fontSize: '20px'
  },
  isShowOnlyOnEarth: false
}

const tooltip = new Tooltip(Cesium, viewer, 'cesium-plugins', tooltipOpts)
```

### `show()`

Used to display a Tooltip that is automatically displayed after the constructor is executed. This function is used in conjunction with the `hide()` function.

```javascript
tooltip.show()
```

### `hide()`

Used to hide Tooltip.

```javascript
tooltip.hide()
```

### `destroy()`

Used to destroy the `Tooltip` instance object.

```javascript
tooltip.destroy()
```
