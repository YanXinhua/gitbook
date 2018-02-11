# 移除点位

## removeMarkerBylayerKey
> <font color=#00aa00>v0.3.0版本已实现删除点位功能</font>
  选择点位后，可根据该点位的id和所在的层id，删除该点位

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
<button id="modifyMap" data-flag="0" style="margin:8px 0px">开启地图编辑</button>
<button id="delFeature" data-flag="0" style="margin:8px 0px">删除点位</button>

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
    position: [113.619942,23.304629],
    markerType: "camera",
    markerName: "test marker",
    imgUrl: "../src/assets/icon.png",
    size: [32, 48]
  });
  $("#modifyMap").on("click", function(e) {
  let flag = $(this).attr("data-flag");
  if (flag === "0") {
    map.openDragTool(
      function(e) {},// translatestart
      function(e) {},// translateend
      function(e) {// select
        if (e.selected.length > 0) {
          let feat = e.selected[0]; //
          selFeatures[feat.id_] = feat.layerKey;
          feat.setStyle(
            new ol.style.Style({
              image: new ol.style.Icon(
                /** @type {olx.style.IconOptions} */ ({
                  src: "../src/assets/u346.png"
                })
              )
            })
          );
        }
      },
      false
    );
    flag = "1";
    $(this).text("关闭地图编辑");
  } else {
    map.closeDragTool();
    flag = "0";
    $(this).text("开启地图编辑");
  }
  $(this).attr("data-flag", flag);
});
$("#delFeature").on("click", function(e) {
  for (let id in selFeatures) {
    map.removeMarkerBylayerKey(id, selFeatures[id]);
  }
  selFeatures = {};
  map.closeDragTool(); //删除点位前，要释放对点位的select
  $("#modifyMap").attr("data-flag", "0");
  $("#modifyMap").text("开启地图编辑");
});
</script>

```javascript
/**
 * 通过marker的id和图层名称移除marker
 * @param id addMarker时，配置的主键
 * @param layerKey 图层名
 */
HDMap.prototype.removeMarkerBylayerKey = function(id, layerKey)
```

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
<button id="modifyMap" data-flag="0" style="margin:8px 0px">开启地图编辑</button>
<button id="delFeature" data-flag="0" style="margin:8px 0px">删除点位</button>
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
    position: [113.619942,23.304629],
    markerType: "camera",
    markerName: "test marker",
    imgUrl: "../src/assets/icon.png",
    size: [32, 48]
  });
  $("#modifyMap").on("click", function(e) {
  let flag = $(this).attr("data-flag");
  if (flag === "0") {
    map.openDragTool(
      function(e) {},// translatestart
      function(e) {},// translateend
      function(e) {// select
        if (e.selected.length > 0) {
          let feat = e.selected[0]; //
          selFeatures[feat.id_] = feat.layerKey;
          feat.setStyle(
            new ol.style.Style({
              image: new ol.style.Icon(
                /** @type {olx.style.IconOptions} */ ({
                  src: "../src/assets/u346.png"
                })
              )
            })
          );
        }
      },
      false
    );
    flag = "1";
    $(this).text("关闭地图编辑");
  } else {
    map.closeDragTool();
    flag = "0";
    $(this).text("开启地图编辑");
  }
  $(this).attr("data-flag", flag);
});
$("#delFeature").on("click", function(e) {
  for (let id in selFeatures) {
    map.removeMarkerBylayerKey(id, selFeatures[id]);
  }
  selFeatures = {};
  map.closeDragTool(); //删除点位前，要释放对点位的select
  $("#modifyMap").attr("data-flag", "0");
  $("#modifyMap").text("开启地图编辑");
});
</script>

```
