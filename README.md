## English | [简体中文](https://github.com/syzdev/cesium-plugins/blob/master/README.zh.md)

## Introduction

Plugins for improving the availability of Cesium.

## Documents

[cesium-plugins documents](https://syzdev.cn/cesium-plugins-docs/)

## Installation

Using npm:

```shell
npm i cesium-plugins
```

Using jsDelivr CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/cesium-plugins@1.0.61/index.js"></script>
```

Using unpkg CDN:

```html
<script src="https://unpkg.com/cesium-plugins@1.0.61/index.js"></script>
```

## Overview

- [PositionPicker](https://syzdev.cn/cesium-plugins-docs/docs/PositionPicker.html)：Plugin for left mouse click to pick up longitude, latitude, and height.

- [Cesium3DTilesLoader](https://syzdev.cn/cesium-plugins-docs/docs/Cesium3DTilesLoader.html)：Plugin for loading and configuring 3DTiles.

- [Tooltip](https://syzdev.cn/cesium-plugins-docs/docs/Tooltip.html)：Plugin for creating tooltip that follow mouse movement.

- [exportSceneAsImage](https://syzdev.cn/cesium-plugins-docs/docs/exportSceneAsImage.html)：Function used to export the scene as an image (.png).

- [FloodAnalysis](https://syzdev.cn/cesium-plugins-docs/docs/FloodAnalysis.html)：Plugin for simulating flood analysis.

- [RotateAroundPoint](https://syzdev.cn/cesium-plugins-docs/docs/RotateAroundPoint.html)：Plugin for camera rotation around a point.

- [WaterMask](https://syzdev.cn/cesium-plugins-docs/docs/WaterMask.html)：Plugin for generating dynamic water surface.

## Usage

Make sure that `Cesium` has been set up and that the `viewer` has been initialized.

The following uses `PositionPicker` as an example to describe the basic usage of `cesium-plugins`.

```javascript
import { PositionPicker } from 'cesium-plugins'
const picker = new PositionPicker(Cesium, viewer)

picker.pick(({ lon, lat, hgt }) => {
  console.log(lon, lat, hgt)
}, true)
```