# 某类点位操作函数

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/jquery/jquery-3.2.1.js" charset="utf-8"></script>
</head>
<div>
	<div id="map" style="width: 100%; height:300px">
    <div id="popup" class="ol-popup">
        <a href="#" id="popup-closer" class="ol-popup-closer"></a>
        <div id="popup-content"></div>
    </div>
  </div>
</div>
<!-- <button id="modifyMap" data-flag="0" style="margin:8px 0px">开启地图编辑</button> -->
<button id="addFeatures" style="margin:8px 0px">添加某类型点位</button>
<button id="hideFeatures" style="margin:8px 0px">隐藏某类型点位</button>
<button id="showFeatures" style="margin:8px 0px">显示某类型点位</button>
<button id="delFeatures" style="margin:8px 0px">删除某类型点位</button>

<script>
  let selFeatures = {};
  var map = new hdmap.initMap({
    gisEngine:'bitmap',
    domId:'map',
    mapUrl:'../src/assets/map.png',
    sizeW: 1024,
    sizeH: 968,
    center:[113.619942,23.304629],
    popupDom:{popup:'popup',popupcloser:'popup-closer',popupcontent:'popup-content'},
    scale: 300
  })
  
map.addMarker({
  id: new Date().valueOf(),
  position: [88.75,14.59375],
  markerType: "guarder",
  name: "test marker",
  imgUrl: "../src/assets/u346.png",
  size: [32, 48]
});

function addMarkers(){
  let posArr = [[-50,50],[80,-30],[-32.75,-6.40625],[37.25,13.09375]]
  for(let i=0,len=posArr.length;i<len;i++){
    map.addMarker({
      id: new Date().valueOf()+i,
      position: [posArr[i][0],posArr[i][1]],
      markerType: "camera",
      name: "test marker",
      imgUrl: "../src/assets/icon.png",
      size: [32, 48]
    });
  }
}
/**添加某一类型的点位*/
$("#addFeatures").on("click", function(e) {
  addMarkers();
});
  
$("#hideFeatures").on("click", function(e) {
  map.hideMarkers("camera");
});
$("#showFeatures").on("click", function(e) {
  map.showMarkers("camera");
});
$("#delFeatures").on("click", function(e) {
  map.removeLayerByLayerKey("cameraLayer");
});

</script>

## hideMarkers

`参数类型`： type

隐藏某一类型点位

实际实现操作是隐藏该类型图层

```javascript
/**
 * HDMap.prototype.hideMarkers
 * 隐藏某类点位
 * @param {String} type 图层类型
 */
HDMap.prototype.hideMarkers = function(type)
```

## showMarkers

显示某一类型点位

```javascript
/**
 * HDMap.prototype.showMarkers
 * 隐藏某类点位
 * @param {String} type 图层类型
 */
HDMap.prototype.showMarkers = function(type)
```

## removeMarkers

从地图上移除一批点位的显示
实际操作是移除这类型点位所在的图层
```javascript
/**
 * HDMap.prototype.showMarkers
 * 隐藏某类点位
 * @param {String} layerKey : 图层id
 */
HDMap.prototype.removeLayerByLayerKey = function(layerKey)
```
**示例：**
```html

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/jquery/jquery-3.2.1.js" charset="utf-8"></script>
</head>
<div>
	<div id="map" style="width: 100%; height:300px">
    <div id="popup" class="ol-popup">
        <a href="#" id="popup-closer" class="ol-popup-closer"></a>
        <div id="popup-content"></div>
    </div>
  </div>
</div>
<!-- <button id="modifyMap" data-flag="0" style="margin:8px 0px">开启地图编辑</button> -->
<button id="addFeatures" style="margin:8px 0px">添加某类型点位</button>
<button id="hideFeatures" style="margin:8px 0px">隐藏某类型点位</button>
<button id="showFeatures" style="margin:8px 0px">显示某类型点位</button>
<button id="delFeatures" style="margin:8px 0px">删除某类型点位</button>

<script>
  let selFeatures = {};
  var map = new hdmap.initMap({
    gisEngine:'bitmap',
    domId:'map',
    mapUrl:'../src/assets/map.png',
    sizeW: 1024,
    sizeH: 968,
    center:[113.619942,23.304629],
    popupDom:{popup:'popup',popupcloser:'popup-closer',popupcontent:'popup-content'},
    scale: 300
  })
  
map.addMarker({
  id: new Date().valueOf(),
  position: [88.75,14.59375],
  markerType: "guarder",
  name: "test marker",
  imgUrl: "../src/assets/u346.png",
  size: [32, 48]
});

function addMarkers(){
  let posArr = [[-50,50],[80,-30],[-32.75,-6.40625],[37.25,13.09375]]
  for(let i=0,len=posArr.length;i<len;i++){
    map.addMarker({
      id: new Date().valueOf()+i,
      position: [posArr[i][0],posArr[i][1]],
      markerType: "camera",
      name: "test marker",
      imgUrl: "../src/assets/icon.png",
      size: [32, 48]
    });
  }
}
/**添加某一类型的点位*/
$("#addFeatures").on("click", function(e) {
  addMarkers();
});
  
$("#hideFeatures").on("click", function(e) {
  map.hideMarkers("camera");
});
$("#showFeatures").on("click", function(e) {
  map.showMarkers("camera");
});
$("#delFeatures").on("click", function(e) {
  map.removeLayerByLayerKey("cameraLayer");
});

</script>

```