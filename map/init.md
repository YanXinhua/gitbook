# 初始化

## initMap

一个简单的地图
<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
</head>

地图引擎在系统运行时已经加载完成，会生成一个全局的hdmap对象，在hdmap上，提供了初始化接口initMap接口
当需要显示一个地图时，只需要根据参数要求传递配置参数，即可进行初始化

|参数名称 | 是否必填 | 参数类型及范围 | 参数说明 |
| :--- | :--- | :--- | :--- |
| gitEngine | 是 | String: baidu, bitmap | 地图引擎类型，百度地图或光栅图 |
| domId | 是 | String | 地图展示的dom节点id |
| mapUrl | bitmap时必填 | String | 光栅图的底图地址 |
| sizeW | bitmap时必填 | Number | 光栅图宽度 |
| sizeH | bitmap时必填 | Number | 光栅图高度 |
| center | 否 | Array | 中心点坐标。GIS地图时如果不填中心为北京，光栅图不填默认为\[0,0\] |
| popupDom | 否 | Object | 填写默认弹窗节点的属性 |
| scale | 是 | Number | 比例尺，默认是1 |
| scaleType | 是 | String | 比例尺类型,默认是 1 |
| popupDom | 是 | Array | 中心点GPS坐标，默认是 \[110.121212, 45.121121\] |
| controlZoom | 否 | Boolean | 地图左上角缩放控件，默认是true |
| attribution | 否 | Boolean | 地图右下角图标信息，默认是false |
| dragPan | 否 | Boolean | 鼠标左键，拖拽地图，默认是true |
| sat | baidu卫星图必传 | Number | 0代表加载普通图层，1代表加载卫星图层，默认为0 |
| zoom | 否 | Number | 缩放级别，bitmap默认是 3，baidu默认是 8 |
| maxZoom | 否 | Number | 缩放级别，bitmap默认是 7，baidu默认是 19 |
| minZoom | 否 | Number | 缩放级别，bitmap默认是 0，baidu默认是 0 |
| minZoom | 否 | Number | 缩放级别，bitmap默认是 3，baidu默认是 8 |


## 光栅图地图示例

<div>
	<div id="map" style="width: 100%; height:300px"></div>
	<script>
        var map = new hdmap.initMap({
            gisEngine:'bitmap',
            domId:'map',
            mapUrl:'../src/assets/map.png',
            sizeW: 1024,
            sizeH: 968,
            center:[113.619942,23.304629]
        })
	</script>
</div>

```html
	<div id="map" style="width: 100%; height:300px"></div>
	<script>
        var map = new hdmap.initMap({
            gisEngine:'bitmap',
            domId:'map',
            mapUrl:'../src/assets/map.png',
            sizeW: 1024,
            sizeH: 968,
            center:[113.619942,23.304629]
        })
	</script>
```

## 百度普通地图示例

<div>
	<div id="map2" style="width: 100%; height:300px"></div>
	<script>
        var map = new hdmap.initMap({
            gisEngine:'baidu',
            domId:'map2',
            sat:0,
            center:[113.619942,23.304629]
        })
	</script>
</div>

```html
	<div id="map2" style="width: 100%"></div>
	<script>
        var map = new hdmap.initMap({
            gisEngine:'baidu',
            domId:'map2',
            sat:0,
            center:[113.619942,23.304629]
        })
	</script>
```

## 百度卫星地图示例

<div>
	<div id="map3" style="width: 100%; height:300px"></div>
	<script>
        var map = new hdmap.initMap({
            gisEngine:'baidu',
            domId:'map3',
            sat:1,
            center:[113.619942,23.304629]
        })
	</script>
</div>

```html
	<div id="map3" style="width: 100%"></div>
	<script>
        var map = new hdmap.initMap({
            gisEngine:'baidu',
            domId:'map3',
            sat:1,
            center:[113.619942,23.304629]
        })
	</script>
```
