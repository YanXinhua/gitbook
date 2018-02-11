# 删除路线

移除路线显示
```javascript
/**
 * HDMap.prototype.removeLineFeature
 * 移除线路信息
 * @param {Object} lineInfo
 * * 线路参数示例
 * {
 *  id: '111' 线路id
 *  name: 'eastArea' 线路名称
 *  lineType: '01' 线路类型
 *  borderPoints: [[[42.5, 94.9375], [41.5, 33.9375], [151, 39.4375], [151.5, 99.4375], [68.5, 112.9375], [42.5, 93.9375]]]
 *    边界点list
 * }
 */
HDMap.prototype.removeLine = function(lineInfo)
```
<head>
	<link href="../src/ol-v4.5.0-dist/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol-v4.5.0-dist/ol-debug.js" charset="utf-8"></script>
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
<button id="removeLine" style="margin-top:15px">删除单个线路</button>

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
  
  var lineList = [
    {
      id: "123",
      name: "安保路线1",
      lineType: "000",
      borderPoints: [
        [-91.5, 34.8203125],
        [57, 22.8203125],
        [-74, -40.6796875]
      ]
    },
    {
      id: "123a",
      name: "安保路线2",
      lineType: "001",
      borderPoints: [
        [-149, 33.40625],
        [-61, 37.4],
        [32, 12],
        [97, 25]
      ],
      lineStyle:{color: "#ff0033",width: 2}
    },
    {
      id: "123b",
      name: "巡更路线1",
      lineType: "002",
      borderPoints: [
        [-172, -8],
        [-105.5, 10],
        [-99, -35],
        [-46.5, -3]
      ],
      lineStyle:{color: "#ffff33",width: 5}
    },
    {
      id: "123c",
      name: "巡更路线2",
      lineType: "002",
      borderPoints: [
        [7.5, -30.09375],
        [73.5, -13.5],
        [85.5, 21.4],
        [147, -33]
      ]
    }
  ]
  var lineStyle = {
      color: "#ff0033",
      width: 10
    };
  // 初始化添加指定路线
  map.addLines(lineList);
  $("#removeLine").on("click", function(e) {
    //
    var feat = map.removeLine(lineList.shift(),lineStyle);
  });
</script>

```html
<head>
	<link href="../src/ol-v4.5.0-dist/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol-v4.5.0-dist/ol-debug.js" charset="utf-8"></script>
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
<button id="removeLine" style="margin-top:15px">删除单个线路</button>

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
  
  var lineList = [
    {
      id: "123",
      name: "安保路线1",
      lineType: "000",
      borderPoints: [
        [-91.5, 34.8203125],
        [57, 22.8203125],
        [-74, -40.6796875]
      ]
    },
    {
      id: "123a",
      name: "安保路线2",
      lineType: "001",
      borderPoints: [
        [-149, 33.40625],
        [-61, 37.4],
        [32, 12],
        [97, 25]
      ],
      lineStyle:{color: "#ff0033",width: 2}
    },
    {
      id: "123b",
      name: "巡更路线1",
      lineType: "002",
      borderPoints: [
        [-172, -8],
        [-105.5, 10],
        [-99, -35],
        [-46.5, -3]
      ],
      lineStyle:{color: "#ffff33",width: 5}
    },
    {
      id: "123c",
      name: "巡更路线2",
      lineType: "002",
      borderPoints: [
        [7.5, -30.09375],
        [73.5, -13.5],
        [85.5, 21.4],
        [147, -33]
      ]
    }
  ]
  var lineStyle = {
      color: "#ff0033",
      width: 10
    };
  // 初始化添加指定路线
  map.addLines(lineList);
  $("#removeLine").on("click", function(e) {
    //
    var feat = map.removeLine(lineList.shift(),lineStyle);
  });
</script>

```

