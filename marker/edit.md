# 编辑点位
> <font color=#00aa00>v0.3.0版本已实现开启、关闭地图编辑功能</font>

用于编辑地图上已经添加的点位信息，拖动更换位置操作

## openDragTool

打开地图的编辑状态，选中点位后，可以拖动地图上点位

```javascript
/*
	打开拖拽工具
	@param dragStartCall：开始拖拽的回调函数
	@param dragEndCall: 结束拖拽的回调函数
	@param selectcall: 选中点位的回调函数
	@param multi : 是否允许选中多个marker，false为不允许，true为允许
  @param dragIngCall: 拖动ing事件回调
  @param isNoDrag: 不允许拖动，不传该值的时候，默认可拖动点位,传值则不可拖动
*/
HDMap.prototype.openDragTool = function(dragStartCall,dragEndCall,selectCall,multi,dragIngCall,isNoDrag)
```

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
<button id="modifyMap" data-flag="0" style="margin-top:15px">开启地图编辑</button>

<script>
  let selFeatures = {};
  var map = new hdmap.initMap({
    gisEngine:'bitmap',
    domId:'map',
    mapUrl:'../src/assets/map.png',
    sizeW: 1024,
    sizeH: 968,
    center:[0.5, -9.6796875],
    popupDom:{popup:'popup',popupcloser:'popup-closer',popupcontent:'popup-content'},
    scale: 300
  })
  map.addMarker({
    id: new Date().valueOf(),
    position: [39, -2.1796875],
    markerType: "camera",
    name: "test marker",
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
</script>

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
    name: "test marker",
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
</script>

```


## closeDragTool

关闭地图编辑状态后，就不可再编辑点位
```javascript
/**
 * 关闭地图编辑状态
 */
HDMap.prototype.closeDragTool = function()
```
