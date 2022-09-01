# 简介

用于提高 Cesium 可用性的插件库。

# 安装

```
npm i cesium-plugins
```

# API

## `PositionPicker`

用于鼠标左键点击拾取经度、纬度和高度。

### `pick(callback, verbose)`

| 名称         | 类型         | 默认值    | 描述               |
| ---------- | ---------- | ------ | ---------------- |
| `callback` | `Function` |        | 获取经度、纬度和高度的回调函数  |
| `verbose`  | `Boolean`  | `true` | 是否在控制台输出经度、纬度和高度 |

```javascript
import { PositionPicker } from 'cesium-plugins'

const picker = new PositionPicker(Cesium, viewer)

picker.pick(({ lon, lat, hgt }) => {
  console.log(lon, lat, hgt)
}, true)
```

### `disable()`

用于销毁`PositionPicker`实例对象。

```javascript
picker.destroy()
```
