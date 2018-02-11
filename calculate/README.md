# 计算工具

地图上的计算接口都放在 hdmap.utils 对象下，使用时，可以直接通过 hdmap.utils.\*\*进行调用

## getDistanceByGPS

> <font color=#00aa00>在 v0.2.0 中已实现</font>

通过两个 GPS 坐标点进行点位距离计算的工具函数

```javascript
/**
 * 通过两点的GPS坐标获取两点间的距离
 * @param {HDMap} 地图对象
 * @param {Array} lonlatA
 * @param {Array} lonlatB
 * @return {Number} 距离 单位m
 */
function getDistanceByGPS(map, lonlatA, lonlatB)
```

## getDistanceByPoint

> <font color=#00aa00>在 v0.5.0 中已实现</font>

通过两点进行点位距离计算的工具函数

```javascript
/**
 * 根据两点的坐标计算两点距离
 * @param {HDMap} 地图对象
 * @param {JSON} lonlats { "lonlatA":[],"lonlatB":[],"lonlatC":[] }
 * @param {JSON} points  { "pointA":[], "pointB":[], "pointC":[] }
 * @return {Number} 距离 单位m
 */
function getDistanceByPoint(map, lonlats, points)
```

## getScaleByGPS

> <font color=#00aa00>在 v0.3.0 中已实现</font>

通过三个 GPS 坐标点和对应的坐标信息进行比例尺计算的工具函数

```javascript
/**
 * 根据三个GPS坐标和对应的坐标信息计算比例尺
 * @param {HDMap} 地图对象
 * @param {JSON} lonlats { "lonlatA":[],"lonlatB":[],"lonlatC":[] }
 * @param {JSON} points  { "pointA":[], "pointB":[], "pointC":[] }
 * @return {Number} scale分母
 */
function getScaleByGPS(map, lonlats, points)
```

## getScaleBySize

> <font color=#00aa00>在 v0.2.0 中已实现</font>

通过地图的长宽和真实长宽进行比例尺计算的工具函数

```javascript
/**
 * 根据地图的长宽和真实长宽进行比例尺计算
 * @param {*} sizeWidth
 * @param {*} sizeHeight
 * @param {*} realWidth
 * @param {*} realHeight
 * @return {Number} scale分母
 */
function getScaleBySize(sizeWidth, sizeHeight, realWidth, realHeight)
```

## getCenterGPS

> <font color=#00aa00>在 v0.3.0 中已实现</font>

通过三个 GPS 点进行中心点计算的工具函数

```javascript
/**
 * 根据三个GPS点进行中心点计算
 * @param {JSON} lonlats { "lonlatA":[],"lonlatB":[],"lonlatC":[] }
 * @param {JSON} points  { "pointA":[], "pointB":[], "pointC":[] }
 * @return {Array}
 */
function getCenterGPS(lonlats, points)
```

## getAreaCenter

获取地图某个区域（多边形）重心

```javascript
/**
 * 获取地图某个区域（多边形）重心
 * @param {Array} points 多边形各点的坐标数组
 * points 格式:[[42.5, 94.9375],[151, 39.4375],[68.5, 112.9375]]
 * @return {Array} areaCenter  重心坐标
 */
function getAreaCenter(points)
```

## getCameraCountPoint

获取摄像头坐标

```javascript
/**
 * 获取摄像头坐标
 * @param {Array} points 形成多边形各点的坐标数组
 * points 格式:[[42.5, 94.9375],[151, 39.4375],[68.5, 112.9375]]
 * @return {Array} cameraCountPoint  摄像头坐标
 */
function getCameraCountPoint(points)
```

## getBroadcastCountPoint

获取广播坐标

```javascript
/**
 * 获取广播坐标
 * @param {Array} points 多边形各点的坐标数组
 * points 格式:[[42.5, 94.9375],[151, 39.4375],[68.5, 112.9375]]
 * @return {Array} broadcastCountPoint  广播坐标
 */
function getBroadcastCountPoint(points)
```

## getWarningConutPoint

获取报警坐标

```javascript
/**
 * 获取报警坐标
 * @param {Array} points 多边形各点的坐标数组
 * points 格式:[[42.5, 94.9375],[151, 39.4375],[68.5, 112.9375]]
 * @return {Array} waringConutPoint  报警坐标
 */
function getWarningConutPoint(points)
```

## 区域重心、摄像头、广播、报警各坐标示例

| 参数名称 | 是否必填 | 参数类型及范围                        | 参数说明           |
| :------- | :------- | :------------------------------------ | :----------------- |
| points   | 是       | Array: [[x1,y1],[x2,y2],[x3,y3].....] | 坐标形成的二维数组 |

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
</head>

<div>
	<div id="map" style="width: 100%; height:300px">
        <div id="popup" class="ol-popup">
            <a href="#" id="popup-closer" class="ol-popup-closer"></a>
            <div id="popup-content"></div>
        </div>
  </div>
	<script>
        window.map = new hdmap.initMap({
            gisEngine:'bitmap',
            domId:'map',
            mapUrl:'../src/assets/map.png',
            sizeW: 1024,
            sizeH: 968,
            center:[110.619942, 25.304629],
            popupDom:{popup:'popup',
            popupcloser:'popup-closer',
            popupcontent:'popup-content'
            },
            scale: 300,
        })
        let polyCoords = [
            [
              [-45.5, 94.9375],
              [-41.5, 33.9375],
              [-151, 39.4375],
              [-151.5, 99.4375],
              [-68.5, 112.9375],
              [-42.5, 93.9375]
             ]
        ]
        let areaCenter = hdmap.utils.getAreaCenter(polyCoords[0]) 
        let cameraCountPoint = hdmap.utils.getCameraCountPoint(polyCoords[0]) 
        let broadcastCountPoint = hdmap.utils.getBroadcastCountPoint(polyCoords[0])
        let warningConutPoint = hdmap.utils.getWarningConutPoint(polyCoords[0]) 
      // console.log(areaCenter)
        let areaInfo = {
          id: 888008,
          name: 'eastArea',
          areaType: '02',
          borderPoints: polyCoords
        }
        let id = new Date().valueOf()
        map.addArea(areaInfo)
        // 固定地图显示区域不受鼠标事件影响
        map.getMap().on('precompose', function() {
          map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
        })
        map.addMarker({
          id: 88800,
          position: areaCenter,
          markerType: 'camera',
          name: id,
          imgUrl: '../src/assets/icon.png',
          size: [32, 48]
        })
        map.addMarker({
          id: 88801,
          position: cameraCountPoint,
          markerType: 'guarder',
          name: id,
          imgUrl: '../src/assets/guard.png',
          size: [36, 48]
        })
        map.addMarker({
          id: 88802,
          position: broadcastCountPoint,
          markerType: 'broadcast',
          name: id,
          imgUrl: '../src/assets/broadcast.png',
          size: [38, 48]
        })
        map.addMarker({
          id: 88803,
          position: warningConutPoint,
          markerType: 'warning',
          name: id,
          imgUrl: '../src/assets//warn.png',
          size: [38, 48]
        })
  </script>

```html
	<div id="map" style="width: 100%; height:300px">
        <div id="popup" class="ol-popup">
            <a href="#" id="popup-closer" class="ol-popup-closer"></a>
            <div id="popup-content"></div>
        </div>
    </div>
	<script>
        let map = new hdmap.initMap({
            gisEngine:'bitmap',
            domId:'map',
            mapUrl:'../src/assets/map.png',
            sizeW: 1024,
            sizeH: 968,
            center:[113.619942,23.304629],
            popupDom:{popup:'popup',popupcloser:'popup-closer',popupcontent:'popup-content'},
            scale: 3000
        })
           let polyCoords = [
            [
              [-45.5, 94.9375],
              [-41.5, 33.9375],
              [-151, 39.4375],
              [-151.5, 99.4375],
              [-68.5, 112.9375],
              [-42.5, 93.9375]
             ]
        ]
        let areaCenter = hdmap.utils.getAreaCenter(polyCoords[0])
        let cameraCountPoint = hdmap.utils.getCameraCountPoint(polyCoords[0])
        let broadcastCountPoint = hdmap.utils.getBroadcastCountPoint(polyCoords[0])
        let warningConutPoint = hdmap.utils.getWarningConutPoint(polyCoords[0])
        let areaInfo = {
          id: 888008,
          name: 'eastArea',
          areaType: '02',
          borderPoints: polyCoords
        }
        let id = new Date().valueOf()
        map.addArea(areaInfo)
         map.getMap().on('precompose', function() {
          map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
        })
        map.addMarker({
          id: 88800,
          position: areaCenter,
          markerType: 'camera',
          name: id,
          imgUrl: '../src/assets/icon.png',
          size: [32, 48]
        })
        map.addMarker({
          id: 88801,
          position: cameraCountPoint,
          markerType: 'guarder',
          name: id,
          imgUrl: '../src/assets/guard.png',
          size: [36, 48]
        })
        map.addMarker({
          id: 88802,
          position: broadcastCountPoint,
          markerType: 'broadcast',
          name: id,
          imgUrl: '../src/assets/broadcast.png',
          size: [38, 48]
        })
        map.addMarker({
          id: 88803,
          position: warningConutPoint,
          markerType: 'warning',
          name: id,
          imgUrl: '../src/assets//warn.png',
          size: [38, 48]
        })
	</script>
```

## judgePointInsidePolygon

## 点位越界 判断一个点是否在多边形内

| 参数名称 | 是否必填 | 参数类型及范围                        | 参数说明               |
| :------- | :------- | :------------------------------------ | :--------------------- |
| point    | 是       | Array: [x,y]                          | 坐标形成的数组         |
| poly     | 是       | Array: [[x1,y1],[x2,y2],[x3,y3].....] | 顶点坐标形成的二维数组 |

```javascript
/**
 * 射线法判断点是否在多边形内部
 * @param {Array} point 待判断的点，格式：[X坐标, Y坐标]
 * @param {Array} poly 多边形顶点，数组成员的格式同 point
 * @return {String} 点 point 和多边形 poly 的几何关系
 */
function judgePointInsidePolygon(point, poly)
```

<script>  
 window.map5 = new hdmap.initMap({
    gisEngine: "bitmap",
    domId: "map5",
    sizeW: 1100,
    sizeH: 600,
    mapUrl: "../src/assets/map.png",
    center: [287, 144],
    popupDom: {
      popup: "popup5",
      popupcloser: "popup-closer5",
      popupcontent: "popup-content5"
    }
  });
  let id = new Date().valueOf();
  map5.addMarker({
    id: 2222,
    position: [-155, 70],
    markerType: "camera",
    name: id,
    imgUrl: "../src/assets/images/icon.png",
    size: [32, 48]
  });
  var polyCoords1 = [
    [
      [-180.5, 94], 
      [-190.5, 33],
      [-151, 39],
      [-151.5, 99],
      [158.5, 112],
      [50,90],
      [-100,-80]
    ]
  ];
  var areaInfo = {
    id: 111,
    name: "eastArea",
    areaType: "01",
    borderPoints: polyCoords1
  };
  map5.addArea(areaInfo);
  </script>

```javascript
<script>
function judgePointInsidePolygon(point, poly) {
  function rayMethod(point, poly) {
    for (var f = false, i = 0, l = poly.length, j = l - 1; i < l; j = i, i++) {
      // 点与多边形顶点重合
      if (
        (poly[i][0] === point[0] && poly[i][1] === point[1]) ||
          (poly[j][0] === point[0] && poly[j][1] === point[1])
      ) {
        return "on";
      }
      // 判断线段两端点是否在射线两侧
      if (
        (poly[i][1] < point[1] && poly[j][1] >= point[1]) ||
          (poly[i][1] >= point[1] && poly[j][1] < point[1])
      ) {
        // 线段上与射线 Y 坐标相同的点的 X 坐标
        var x = poly[i][0] + (point[1] - poly[i][1]) *(poly[j][0] - poly[i][0]) /
          (poly[j][1] - poly[i][1]);
        // 点在多边形的边上
        if (x === point[0]) {
          return "on";
        }
        // 射线穿过多边形的边界
        if (x > point[0]) {
          f = !f;
        }
      }
    }
    // 射线穿过多边形边界的次数为奇数时点在多边形内
    return f ? "in" : "out";
  }
  // console.log(poly);
  var result = rayMethod(point, poly);
  return result;
  // console.log(result);
}
  hdmap.utils.judgePointInsidePolygon([-155, 70],
  [
    [-180.5, 94],
    [-190.5, 33],
    [-151, 39],
    [-151.5, 99],
    [158.5, 112],
    [50,90],
    [-100,-80]
  ]
  );  
};
</script>
```



