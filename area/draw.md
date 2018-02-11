# 区域绘制

这个操作是在地图上新增区域时的操作

新增区域操作时需要先打开地图画线工具，进入画线编辑状态，然后在地图上进行路线绘制，在最后一点双击即可完成区域绘制

> 注意这里和路线绘制不同的是，起始点会进行划线关联

## openDrawShapeTool

打开画图工具，进入图形绘制状态

**参数**

`type` Circle(圆) || Box（矩形） || Polygon（多边形）

`drawendCall` 绘制结束的回调

`modifyendCall` 修改图形的回调

```javascript
/**
 *框选，圈选,多边形绘制
 * @param {*} type : Circle(圆) || Box（矩形） || Polygon（多边形）
 * @param {*} drawendCall 绘制结束的回调
 * @param {*} modifyendCall 修改图形的回调
 */
HDMap.prototype.openDrawShapeTool = function(type, drawendCall, modifyendCall)
```

## closeDrawShapeTool

> 退出图形绘制状态

调用此方法放弃绘制，结束绘制状态
```javascript
/*
	结束绘制状态
*/
HDMap.prototype.closeDrawShapeTool = function()
```

## showDrawShape

> 图形绘制结束后，调用此方法把图形在gisLayer层上显示出来，此方法返回所绘制的图形AreaFeature对象

```javascript
/**
 * 编辑完图形后，调用此方法，把图形以AreaFeature类型显示在gisLayer上，并返回AreaFeature对象
 * @param {Object|Array|undefined} option 
 1、option:Object : 是一个区域数据对象,调用此方法返回一个AreaFeature对象
 2、option:Array : 是一个存放多个‘区域数据对象’的数组,调用此方法返回一个存放所有所画图形(AreaFeature对象)的数组
 3、option:undefined : 不传参,调用此方法返回一个存放所有所画图形(AreaFeature对象)的数组
 * 区域数据对象示例
 * {
 *  id: '111' 区域id
 *  name: 'eastArea' 区域名称
 *  areaType: '01' 区域类型
 * }
 */
HDMap.prototype.showDrawShape = function(option)
```

## editDrawShape

> 传入一个区域数据对象，可对此图形进行编辑

```javascript
/**
 * 重新编辑之前画的图形
 * @param {*} option 区域数据对象
 * 区域数据对象示例:
 * {
 *  id: '111' 区域id
 *  name: 'eastArea' 区域名称
 *  areaType: '01' 区域类型
 *  borderPoints: [[[42.5, 94.9375], [41.5, 33.9375], [151, 39.4375], [151.5, 99.4375], [68.5, 112.9375], [42.5, 93.9375]]] 边界点list
 *  areaTypeOf: 'parking' 此AreaFeature属于停车场图形类型，调用此方法只能对图形进行缩放、旋转编辑
    rotate: 0 AreaFeature 图形的旋转弧度
 * }
 */
HDMap.prototype.editDrawShape = function(option) 
```

## clearDrawShape

> 清空当前画图层上的所有图形数据

```javascript
/**
 * 清空画图层的图形
 * 注意：该方法会清空当前画图层上的所有图形
 */
HDMap.prototype.clearDrawShape = function ()

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
<button id="drawShapeTool" data-flag="0" style="margin-top:15px">开启画图状态</button>
<button id="saveDrawShape" style="margin-top:15px">保存刚画的图形</button>
<button id="editDrawShape" style="margin-top:15px">编辑刚画的图形</button>

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
  var option = {
    id: "123bbb",
    name: "testareaf",
    areaType: "001",
    borderPoints: [
      [
        [-115, -26.703125],
        [-56.5, 55.796875],
        [92, 10.296875],
        [63.5, -53.703125],
        [-115, -26.703125]
      ]
    ]
  };
  
  $("#drawShapeTool").on("click", function(e) {
    var flag = $(this).attr("data-flag")
    if(flag=="0"){
      map.openDrawShapeTool("Polygon",function(e){
        console.log(e);// drawend
      },function(e){
        console.log(e);// modifyend
      })
      $(this).attr("data-flag","1")
      $(this).text("关闭画图工具")
    }else{
      map.closeDrawLineTool();
      $(this).attr("data-flag","0")
      $(this).text("开启画图工具")
    }
  });
  $("#saveDrawShape").on("click", function(e) {
    map.closeDrawShapeTool();
    $("#drawShapeTool").attr("data-flag","0")
    $("#drawShapeTool").text("开启画图工具")
    var feat = map.showDrawShape(option);
    option.borderPoints = feat.getGeometry().getCoordinates();
    console.log(option.borderPoints)
  });
  $("#editDrawShape").on("click", function(e) {
    $("#drawShapeTool").attr("data-flag","1")
    $("#drawShapeTool").text("关闭画图工具")
    map.editDrawShape(option);
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
<button id="drawShapeTool" data-flag="0" style="margin-top:15px">开启画图状态</button>
<button id="saveDrawShape" style="margin-top:15px">保存刚画的图形</button>
<button id="editDrawShape" style="margin-top:15px">编辑刚画的图形</button>

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
  var option = {
    id: "123bbb",
    name: "testareaf",
    areaType: "001",
    borderPoints: [
      [
        [12569999.832246065, 2737852.923916945],
        [12824993.758605413, 2712781.578639407],
        [12676400.17561903, 2552569.5673536775],
        [12569999.832246065, 2737852.923916945]
      ]
    ]
  };
  
  $("#drawShapeTool").on("click", function(e) {
    var flag = $(this).attr("data-flag")
    if(flag=="0"){
      map.openDrawShapeTool("Polygon",function(e){
        console.log(e);// drawend
      },function(e){
        console.log(e);// modifyend
      })
      $(this).attr("data-flag","1")
      $(this).text("关闭画图工具")
    }else{
      map.closeDrawLineTool();
      $(this).attr("data-flag","0")
      $(this).text("开启画图工具")
    }
  });
  $("#saveDrawShape").on("click", function(e) {
    map.closeDrawShapeTool();
    $("#drawShapeTool").attr("data-flag","0")
    $("#drawShapeTool").text("开启画图工具")
    var feat = map.showDrawShape(option);
    option.borderPoints = feat.getGeometry().getCoordinates();
    console.log(option.borderPoints)
  });
  $("#editDrawShape").on("click", function(e) {
    $("#drawShapeTool").attr("data-flag","1")
    $("#drawShapeTool").text("关闭画图工具")
    map.editDrawShape(option);
  });
</script>

```