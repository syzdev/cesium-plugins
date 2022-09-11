# [English](./README.md) | 简体中文

# 简介

用于提高Cesium可用性的插件库。

# 安装

使用 npm：

```
npm i cesium-plugins
```

使用 jsDelivr CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/cesium-plugins@1.0.48/index.js"></script>
```

使用 unpkg CDN:

```html
<script src="https://unpkg.com/cesium-plugins@1.0.48/index.js"></script>
```

# 目录

- [PositionPicker](https://github.com/syzdev/cesium-plugins/blob/master/README.zh.md#positionpicker)：用于鼠标左键点击拾取经度、纬度和高度的工具类。

- [Cesium3DTilesLoader](https://github.com/syzdev/cesium-plugins/blob/master/README.zh.md#cesium3dtilesloader)：用于加载并配置3DTiles的工具类。

- [Tooltip](https://github.com/syzdev/cesium-plugins/blob/master/README.zh.md#tooltip)：用于创建跟随鼠标移动的Tooltip工具类。

- [exportSceneAsImage](https://github.com/syzdev/cesium-plugins/blob/master/README.zh.md#exportSceneAsImage)：用于将场景导出为图片（.png）的方法。

- [FloodAnalysis](https://github.com/syzdev/cesium-plugins/blob/master/README.zh.md#FloodAnalysis)：用于模拟淹没分析的工具类。

# API

## PositionPicker

用于鼠标左键点击拾取经度、纬度和高度的工具类。

在线示例：[PositionPicker](https://syzdev.cn/cesium-plugins/example/PositionPicker.html)（在浏览器控制台查看输出）

### `constructor(Cesium, viewer)`

构造函数，用于初始化`PositionPicker`实例对象。

| 名称       | 类型       | 默认值 | 描述                   |
| -------- | -------- | --- | -------------------- |
| `Cesium` | `Object` |     | Cesium全局对象           |
| `viewer` | `Object` |     | 初始化Cesium场景的`viewer` |

```javascript
import { PositionPicker } from 'cesium-plugins'
const picker = new PositionPicker(Cesium, viewer)
```

### `pick(callback, verbose)`

核心方法，用于鼠标左键点击拾取经度、纬度和高度。获取的经度、纬度和高度可在回调函数`callback`中获取。

| 名称         | 类型         | 默认值    | 描述               |
| ---------- | ---------- | ------ | ---------------- |
| `callback` | `Function` |        | 获取经度、纬度和高度的回调函数  |
| `verbose`  | `Boolean`  | `true` | 是否在控制台输出经度、纬度和高度 |

```javascript
picker.pick(({ lon, lat, hgt }) => {
  console.log(lon, lat, hgt)
}, true)
```

### `destroy()`

用于销毁`PositionPicker`实例对象。

```javascript
picker.destroy()
```

## Cesium3DTilesLoader

用于加载并配置3DTiles的工具类。

在线示例：[Cesium3DTilesLoader](https://syzdev.cn/cesium-plugins/example/Cesium3DTilesLoader.html)

### `constructor(Cesium, viewer)`

构造函数，用于初始化`Cesium3DTilesLoader`实例对象。

| 名称       | 类型       | 默认值 | 描述                   |
| -------- | -------- | --- | -------------------- |
| `Cesium` | `Object` |     | Cesium全局对象           |
| `viewer` | `Object` |     | 初始化Cesium场景的`viewer` |

```javascript
import { Cesium3DTilesLoader } from 'cesium-plugins'
const loader = new Cesium3DTilesLoader(Cesium, viewer)
```

### `load(url, posOpts, loadOpts): Cesium3DTileset `

核心方法，用于加载并配置3DTiles。

| 名称         | 类型       | 默认值   | 描述                                                |
| ---------- | -------- | ----- | ------------------------------------------------- |
| `url`      | `String` |       | 3DTiles的`tileset.json`资源路径                        |
| `posOpts`  | `Object` | （见下文） | 加载3DTiles的位置、旋转和缩放参数                              |
| `loadOpts` | `Object` | （见下文） | 加载3DTiles的配置项，与`Cesium3DTileset`类的`option`配置项保持一致 |

该方法会返回一个`Cesium3DTileset`实例对象。

`posOpts`的参数列表及默认配置如下：

```javascript
{
  lon: 116.391311, // 模型经度（单位：十进制）
  lat: 39.90616, // 模型纬度（单位：十进制）
  hgt: 0, // 模型高度（单位：米）
  rx: 0, // x轴（经度）方向旋转角度（单位：度）
  ry: 0, // y轴（纬度）方向旋转角度（单位：度）
  rz: 0, // z轴（高程）方向旋转角度（单位：度）
  scale: 1, // 缩放比例
},
```

`loadOpts`与`Cesium3DTileset`类的`option`配置项保持一致，详见[Cesium3DTileset - Cesium Documentation](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileset.html?classFilter=Cesium3DTileset#Cesium3DTileset)，如可以添加如下配置：

```javascript
{
  maximumScreenSpaceError: 256,
  maximumMemoryUsage: 5120,
  immediatelyLoadDesiredLevelOfDetail: true,
}
```

完整示例：

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

用于将视角定位到所加载的3DTiles上。

```javascript
loader.locate()
```

### `destroy()`

用于销毁`Cesium3DTilesLoader`实例对象。

```javascript
loader.destroy()
```

## Tooltip

用于创建跟随鼠标移动的Tooltip工具类。

在线示例：[Tooltip](https://syzdev.cn/cesium-plugins/example/Tooltip.html)

### `constructor(Cesium, viewer, msg, tooltipOpts)`

构造函数，用于初始化`Tooltip`实例对象。

| 名称            | 类型       | 默认值   | 描述                      |
| ------------- | -------- | ----- | ----------------------- |
| `Cesium`      | `Object` |       | Cesium全局对象              |
| `viewer`      | `Object` |       | 初始化Cesium场景的`viewer`    |
| `msg`         | `String` |       | Tooltip中显示的字符           |
| `tooltipOpts` | `Object` | （见下文） | 与Tooltip有关的配置项，如位置、样式等。 |

```javascript
import { Tooltip } from 'cesium-plugins'
const tooltip = new Tooltip(Cesium, viewer, 'cesium-plugins', tooltipOpts)
```

`tooltipOpts`的参数列表及默认配置如下：

```javascript
{
  // Tooltip距离鼠标的偏移量（单位：px）
  offset: {
    left: 30,
    top: 50,
  },
  // Tooltip容器的样式
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
  // Tooltip内容的样式
  innerStyle: {
    padding: '5px 8px',
    fontSize: '10px',
    fontWeight: '400',
  },
  // 是否仅当鼠标在地球上时显示Tooltip
  isShowOnlyOnEarth: true,
}
```

完整示例：

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

用于显示Tooltip，在执行构造函数后，Tooltip便会自动显示，该方法的作用在于配合`hide()`方法一起使用。

```javascript
tooltip.show()
```

### `hide()`

用于隐藏Tooltip。

```javascript
tooltip.hide()
```

### `destroy()`

用于销毁`Tooltip`实例对象。

```javascript
tooltip.destroy()
```

## exportSceneAsImage

用于将场景导出为图片（.png）的方法。

在线示例：[exportSceneAsImage](https://syzdev.cn/cesium-plugins/example/exportSceneAsImage.html)

| 名称         | 类型       | 默认值                             | 描述                   |
| ---------- | -------- | ------------------------------- | -------------------- |
| `viewer`   | `Object` |                                 | 初始化Cesium场景的`viewer` |
| `fileName` | `String` | `Scene-${new Date().getTime()}` | 导出的文件名               |

```javascript
import { exportSceneAsImage } from 'cesium-plugins'
exportSceneAsImage(viewer, 'example-file-name')
```

## FloodAnalysis

用于模拟淹没分析的工具类。

在线示例：[FloodAnalysis](https://syzdev.cn/cesium-plugins/example/FloodAnalysis.html)

> 注意：使用该工具类时，请确保场景中加载了地形，并且开启了地形深度检测。
> 
> ```javascript
> viewer.terrainProvider = Cesium.createWorldTerrain()
> viewer.scene.globe.depthTestAgainstTerrain = true
> ```

### `constructor(Cesium, viewer, pos, floodOpts)`

构造函数，用于初始化`FloodAnalysis`实例对象。

| 名称          | 类型       | 默认值   | 描述                                            |
| ----------- | -------- | ----- | --------------------------------------------- |
| `Cesium`    | `Object` |       | Cesium全局对象                                    |
| `viewer`    | `Object` |       | 初始化Cesium场景的`viewer`                          |
| `pos`       | `Array`  | （见下文） | 用于模拟淹没分析的经纬度区域范围                              |
| `floodOpts` | `Object` | （见下文） | 与floodOpts有关的配置项，如初始水位高度，目标水位高度，水位上升速度，水的颜色等。 |

```javascript
import { PositionPicker } from 'cesium-plugins'
const flood = new FloodAnalysis(Cesium, viewer, pos, floodOpts)
```

`pos`的配置样例如下：

```javascript
const pos = [
  85.122, 28.848, 
  85.074, 28.309, 
  86.037, 28.257, 
  86.044, 28.835
]
```

`floodOpts`的参数列表及默认配置如下：

```javascript
{
  waterHeight: 0, // 单位：米
  targetWaterHeight: 100, // 单位：米
  speed: 1, // 单位：米
  waterColor: new Cesium.Color.fromBytes(64, 157, 250, 120),
}
```

其中`waterColor`需要是Cesium中定义的颜色，详见：[Color - Cesium Documentation](https://cesium.com/learn/cesiumjs/ref-doc/Color.html?classFilter=color)。

### `start(callback)`

用于开始模拟淹没分析。

| 名称         | 类型         | 默认值 | 描述            |
| ---------- | ---------- | --- | ------------- |
| `callback` | `Function` |     | 获取当前水位高度的回调函数 |

```javascript
flood.start((waterHeight) => {
  // console.log(waterHeight)
})
```

### `pause()`

用于暂停模拟淹没分析。

```javascript
flood.pause()
```

### `destroy()`

用于销毁场景中的模拟淹没分析。

```javascript
flood.destroy()
```

### `getCurrentWaterHeight()`

用于获取当前的水位高度。

```javascript
flood.getCurrentWaterHeight()
```



### `setCurrentWaterHeight(height)`

用于设置当前的水位高度。

| 名称       | 类型       | 默认值 | 描述             |
| -------- | -------- | --- | -------------- |
| `height` | `Number` |     | 设置当前的水位高度，单位：米 |

```javascript
flood.setCurrentWaterHeight(1000)
```
