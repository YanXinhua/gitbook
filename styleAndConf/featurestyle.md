# 点位样式

## getFeatureStyle()

> <font color=#00aa00>在 v0.3.0 中已实现</font>

```javascript
/**
   * 获取默认点位样式
   * @param {Object} markerInfo 点位信息
   * 参数示例：
   * {
   *  id: 333,
      position: [-50, 0],
      markerType: "guarder",
      markerName: id,
      imgUrl: "./assets/images/u4828.png",
      size: [32, 48]
   * }
   * @param {Object} styleObj 如需自定义样式，则传
   * @return {Object} 样式
   */
getFeatureStyle(markerInfo, styleObj)
```

## getCountCameraFeatureStyle()

> <font color=#00aa00>在 v0.4.0 中已实现</font>

```javascript
/**
   * 获取摄像头统计点样式
   * @param {Object} markerInfo 点位信息
   */
getCountCameraFeatureStyle(text)
```

## getCountWarningFeatureStyle()

> <font color=#00aa00>在 v0.4.0 中已实现</font>

```javascript
/**
   * 获取报警统计点样式
   * @param {Object} markerInfo 点位信息
   */
getCountWarningFeatureStyle(markerInfo)
```
## getCountBroadcastFeatureStyle()

> <font color=#00aa00>在 v0.4.0 中已实现</font>

```javascript
/**
   * 获取广播统计点样式
   * @param {Object} markerInfo 点位信息
   */
getCountBroadcastFeatureStyle(text)
```
## 点位操作方法

```html
<!-- 点位操作方法（前提：地图已初始化成功） -->
  export default {
    data () {
      return {
        bitmap : null
      }
    },
    mounted: {
      <!-- 初始化方法详见方法 initMap() -->
      this.bitmap = new hdmap.initMap({
        gisEngine: 'bitmap',
        sizeW: 1920,
        sizeH: 1080,
        domId: 'bitmap',
        mapUrl: '../src/assets/u768.jpg',
        maxZoom: 3,
        minZoom: 3,
        center: [112.334403, 39.8],
        popupDom: {
          popup: 'popup',
          popupcloser: 'popup-closer',
          popupcontent: 'popup-content'
        }
      })
    }
  }
1.添加点位（调用方法： addMarker(markerInfo)）
  this.bitmap.addMarker({
    id: 111,
    position: [30, 20],
    markerType: 'camera',
    markerName: '222',
    imgUrl: '../src/assets/icon.png',
    size: [32, 48]
  })
2.更新点位（调用方法：updateMarker(markerInfo, styleObj)）
  2.1 使用默认点位样式
  this.bitmap.updateMarker({
    id: 111,
    position: [80, 100],
    markerType: 'broadcast',
    markerName: '222',
    imgUrl: '../src/assets/u888.png',
    size: [50, 40]
  })
  2.2 自定义点位样式，需传入 styleObj
  this.bitmap.updateMarker({
    id: 111,
    position: [80, 100],
    markerType: 'broadcast',
    markerName: '222',
    imgUrl: '../src/assets/u888.png',
    size: [50, 40]
  }, {
    color: 'red', 选填
    scale: 2,  选填
    opacity: 0.8  选填
  })
3.删除点位（调用方法：removeMarker（markerInfo））
  this.bitmap.removeMarker({
    id: 111, // 必填
    position: [80, 100],
    markerType: 'broadcast', // 必填
    markerName: '222',
    imgUrl: '../src/assets/u888.png',
    size: [50, 40]
  })
4.批量添加点位（调用方法：addMarkers(markerList)）
  this.bitmap.addMarkers(markerList)
5.隐藏点位（调用方法：hideMarkers（markerType））
  this.bitmap.hideMarkers('broadcast')
6.显示点位（调用方法：showMarkers（markerType））
  this.bitmap.showMarkers('broadcast')
7.添加统计点位（调用方法：addCountMarker（markerInfo））
  this.bitmap.addCountMarker({
    id: 22, 必填
    name: 22,
    markerType: 'countCamera', 必填
    position: [0, 10], 必填
    url: '../assets/images/u349.png', 必填
    baseUrl: '../assets/images/u887.png', 必填
    cameraNum: '9' 
  })
8.隐藏统计点位（调用方法：hideCountMarkers（markerType））
  this.bitmap.hideCountMarkers('countCamera')
9.显示统计点位（调用方法：showCountMarkers（markerType））
  this.bitmap.showCountMarkers('countCamera')
```

