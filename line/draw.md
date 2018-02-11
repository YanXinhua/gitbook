# 路线绘制

新增操作需要先打开地图画线工具，进入画线编辑状态，然后在地图上进行路线绘制，在最后一点双击即可完成路线绘制

## openDrawLineTool

打开画线工具，进入划线状态
```javascript
/**
 * 打开画线工具，可以画线
 * @param {*} lineStyle 线的样式,具体都有什么样式参考api中的ol.style.Stroke，例如：{color:'#ffcc33',width:2}
 * @param {*} pointStyle 如果positioncall传值时，这里必须传值，具体传值参考例子ol.style.Circle或者ol.style.Icon
 * @param {*} positioncall 自己写的点位置计算函数，比如我们想要在线的中间加点，则需要写此函数，参数为start,end 即一条线的起点和终点坐标
 * @param {*} drawendCall 画结束的回调函数
 * @param {*} modifyCall 修改画线的回调函数
 */
HDMap.prototype.openDrawLineTool = function (lineStyle, pointStyle, positioncall, drawendCall, modifyCall)
```

**参数**

`lineStyle` 线的样式,具体都有什么样式参考api中的ol.style.Stroke

`callback` 划线完成的回调函数

`positioncall` 自己写的点位置计算函数，比如我们想要在线的中间加点，则需要写词函数，参数为start,end 即一条线的起点和终点坐标

`pointStyle` 如果positioncall传值时，这里必须传值，具体传值参考例子ol.style.Circle或者ol.style.Icon

## closeDrawLineTool

退出划线状态
```javascript
/*
	关闭划线工具,同时清理图层和feature
*/
HDMap.prototype.closeDrawLineTool = function()
```

## 保存画线，并把画线在lineLayer层上显示出来
```javascript
/**
 * 编辑完线路后，调用此方法，把线路显示在gisLayer上，并返回Feature对象
 * @param {*} option 线路参数示例
 * {
 *  id: '111' 线路id
 *  name: 'lineName' 线路名称
 *  markerType: '01' 线路类型
 * }
 */
HDMap.prototype.showDrawLine = function (option)
```
## 编辑画线
```javascript
/**
 * 重新编辑之前画的线路
 * @param {*} option
 * * 线路数据对象示例:
 * {
 *  id: '111' 线路id
 *  name: 'eastArea' 线路名称
 *  lineType: '01' 线路类型
 *  borderPoints: [[[42.5, 94.9375], [41.5, 33.9375], [151, 39.4375], [151.5, 99.4375], [68.5, 112.9375], [42.5, 93.9375]]]  边界点list
 * }
 * @param {*} lineStyle 线的样式,具体都有什么样式参考api中的ol.style.Stroke，例如：{color:'#ffcc33',width:2}
 * @param {*} pointStyle 如果positioncall传值时，这里必须传值，具体传值参考例子ol.style.Circle或者ol.style.Icon
 * @param {*} positioncall 自己写的点位置计算函数，比如我们想要在线的中间加点，则需要写此函数，参数为start,end 即一条线的起点和终点坐标
 * @param {*} drawendCall 画结束的回调函数
 * @param {*} modifyCall 修改画线的回调函数
 */
HDMap.prototype.editDrawLine = function (option, lineStyle, pointStyle, positioncall, drawendCall, modifyCall)
```

> 如果每次划线成功之后就有业务处理，可以在划线回调中调用函数退出划线状态


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
<button id="drawLineTool" data-flag="0" style="margin-top:15px">开启画线状态</button>
<button id="saveDrawLine" style="margin-top:15px">保存刚画的线路</button>
<button id="editDrawLine" style="margin-top:15px">编辑刚画的路线</button>

<script>
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
  var optionLine = {
    id: "123bbb",
    name: "testareaf",
    lineType: "003",
    borderPoints: [
      [-91.5, 34.8203125],
      [57, 22.8203125],
      [-74, -40.6796875]
    ]
  };
  var lineStyle = {
      color: "#ff0033",
      width: 10
    };
  $("#drawLineTool").on("click", function(e) {
    var flag = $(this).attr("data-flag")
    if(flag=="0"){
      map.openDrawLineTool({ color: "#ff0033", width: 2 },null,null,
      function(e){
        console.log(e);// drawend
      },function(e){
        console.log(e);// modifyend
      })
      $(this).attr("data-flag","1")
      $(this).text("关闭画线工具")
    }else{
      map.closeDrawLineTool();
      $(this).attr("data-flag","0")
      $(this).text("开启画线工具")
    }
  });
  $("#saveDrawLine").on("click", function(e) {
    map.closeDrawLineTool();
    $("#drawLineTool").attr("data-flag","0")
    $("#drawLineTool").text("开启画线工具")
    var feat = map.showDrawLine(optionLine,lineStyle);
    optionLine.borderPoints = feat.getGeometry().getCoordinates();
    console.log(optionLine.borderPoints)
  });
  $("#editDrawLine").on("click", function(e) {
    $("#drawLineTool").attr("data-flag","1")
    $("#drawLineTool").text("关闭画线工具")
    map.editDrawLine(optionLine, { color: "#00f033", width: 2 });
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
<button id="drawLineTool" data-flag="0" style="margin-top:15px">开启画线状态</button>
<button id="saveDrawLine" style="margin-top:15px">保存刚画的线路</button>
<button id="editDrawLine" style="margin-top:15px">编辑刚画的路线</button>

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
  var optionLine = {
    id: "123bbb",
    name: "testareaf",
    lineType: "003",
    borderPoints: [
      [-91.5, 34.8203125],
      [57, 22.8203125],
      [-74, -40.6796875]
    ]
  };
  var lineStyle = {
      color: "#ff0033",
      width: 10
    };
  $("#drawLineTool").on("click", function(e) {
    var flag = $(this).attr("data-flag")
    if(flag=="0"){
      map.openDrawLineTool({ color: "#ff0033", width: 2 },null,null,
      function(e){
        console.log(e);// drawend
      },function(e){
        console.log(e);// modifyend
      })
      $(this).attr("data-flag","1")
      $(this).text("关闭画线工具")
    }else{
      map.closeDrawLineTool();
      $(this).attr("data-flag","0")
      $(this).text("开启画线工具")
    }
  });
  $("#saveDrawLine").on("click", function(e) {
    map.closeDrawLineTool();
    var feat = map.showDrawLine(optionLine,lineStyle);
    optionLine.borderPoints = feat.getGeometry().getCoordinates();
  });
  $("#editDrawLine").on("click", function(e) {
    map.editDrawLine(optionLine, { color: "#00f033", width: 2 });
  });
</script>


```
