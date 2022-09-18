## [English](./README.md) | 简体中文

## 简介

用于提高Cesium可用性的插件库。

## 文档

[cesium-plugins 文档](https://syzdev.cn/cesium-plugins-docs/zh/)

## 安装

使用 npm：

```shell
npm i cesium-plugins
```

使用 jsDelivr CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/cesium-plugins@1.0.5/index.js"></script>
```

使用 unpkg CDN:

```html
<script src="https://unpkg.com/cesium-plugins@1.0.5/index.js"></script>
```

## 目录

- [PositionPicker](https://syzdev.cn/cesium-plugins-docs/zh/docs/PositionPicker.html)：用于鼠标左键点击拾取经度、纬度和高度的工具类。

- [Cesium3DTilesLoader](https://syzdev.cn/cesium-plugins-docs/zh/docs/Cesium3DTilesLoader.html)：用于加载并配置3DTiles的工具类。

- [Tooltip](https://syzdev.cn/cesium-plugins-docs/zh/docs/Tooltip.html)：用于创建跟随鼠标移动的Tooltip工具类。

- [exportSceneAsImage](https://syzdev.cn/cesium-plugins-docs/zh/docs/exportSceneAsImage.html)：用于将场景导出为图片（.png）的方法。

- [FloodAnalysis](https://syzdev.cn/cesium-plugins-docs/zh/docs/FloodAnalysis.html)：用于模拟淹没分析的工具类。

- [RotateAroundPoint](https://syzdev.cn/cesium-plugins-docs/zh/docs/RotateAroundPoint.html)：用于相机绕点旋转的工具类。

## 基本示例

请确保项目中`Cesium`已经成功引入，并且`viewer`已经完成初始化。

下面以`PositionPicker`为例描述`cesium-plugins`的基本用法。

```javascript
import { PositionPicker } from 'cesium-plugins'
const picker = new PositionPicker(Cesium, viewer)

picker.pick(({ lon, lat, hgt }) => {
  console.log(lon, lat, hgt)
}, true)
```