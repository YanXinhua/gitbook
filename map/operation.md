# 操作函数

这里介绍一些在地图的操作过程中会用到的一些常用函数

## setCenter

> <font color=#00aa00>在 v0.1.0 中已实现</font>

设置地图中心点

```javascript
/**
 * HDMap.prototype.setCenter
 * 为地图提供定位功能，coordinate为坐标数组 元素[0] 为x  元素[1]为y
 * @param {Array} coordinate 点位坐标
 * 如果百度地图想要使用此方法，需要先将经纬度用提供的方法转换成米坐标系，再传入参数
 * @param {number} zoom 参数是放大倍数，如果不填则不会进行放大，只定位
 */
HDMap.prototype.setCenter = function(
  /*type : ol.Coordinate*/ coordinate,
  zoom
)
```

## getCenter

> <font color=#00aa00>在 v0.1.0 中已实现</font>

获取当前地图中心点

```javascript
/**
 * HDMap.prototype.getCenter
 * 获取目前地图的中心点
 * @return {Array}
 */
HDMap.prototype.getCenter = function() {
  return this._map.getView().getCenter()
}
```

## setZoom

> <font color=#00aa00>在 v0.2.0 中已实现</font>
>
> 如果设置的 zoom 值大于 maxZoom 或者小于 minZoom，将取设置的边界值进行设置

设置当前地图放大等级

```javascript
/**
 * HDMap.prototype.setZoom
 * 设置地图的放大倍数
 * 当大于最大值时，使用maxZoom，小于minZoom，使用minZoom
 * @param {number} zoom
 */
HDMap.prototype.setZoom = function(zoom)
```

## getZoom

> <font color=#00aa00>在 v0.2.0 中已实现</font>

获取当前地图的放大等级

```javascript
/**
 * HDMap.prototype.getZoom
 * 得到目前地图的放大倍数
 * @return {number}
 */
HDMap.prototype.getZoom = function() {
  return this._map.getView().getZoom()
}
```

#示例

<html lang="en">

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
  <link href="../src/hdmap/hdmap.css" rel="stylesheet" type="text/css" />
  <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
  <script src="../src/vue/vue.js"></script>  
  <script src="https://unpkg.com/element-ui/lib/index.js"></script>
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
  <style>
   .row{
      margin-top:4px;
    }
  </style>
</head>
<body>
  <div id="app">
    <div id="bitmap"></div>
    <el-row class='row'>
      <el-col :span="3">
        <el-button type="primary" @click='setCenter'>设置地图中心</el-button>
         </el-col>
      <el-col :span="20" offset="1">
        <el-input v-model="input" placeholder="请输入坐标数组如[x,y]" ></el-input>
      </el-col>
    </el-row>
    <el-row class='row'>
      <el-col :span="3">
        <el-button type="success"  @click='getCenter'>获取地图中心</el-button>
         </el-col>
      <el-col :span="20" offset="1">
        <el-input v-model="input1"></el-input>
      </el-col>
    </el-row>
    <el-row class='row'>
      <el-col :span="3">
        <el-button type="warning"  @click='setZoom'>设置放大等级</el-button>
         </el-col>
      <el-col :span="20" offset="1">
        <el-input v-model="zoom" placeholder="请输入地图放大倍数"></el-input>
      </el-col>
    </el-row>
     <el-row class='row'>
      <el-col :span="3">
        <el-button type="danger"  @click='getZoom'>获取放大等级</el-button>
         </el-col>
      <el-col :span="20" offset="1">
        <el-input v-model="getzoom" ></el-input>
      </el-col>
    </el-row>
  </div>

</body>

<script>
  new Vue({
    el: '#app',
    data: {
      input: [],
      input1: [],
      zoom: '',
      getzoom: ''
    },
    methods: {
      setCenter(){
        let input = JSON.parse(this.input)
        this.bitmap.setCenter(input)
      },
      getCenter(){
        this.input1 = JSON.stringify(this.bitmap.getCenter());
      },
      setZoom(){
        let zoom = JSON.parse(this.zoom)
        this.bitmap.setZoom(zoom)
      },
      getZoom(){
        this.getzoom = this.bitmap.getZoom();
      }
    },
    mounted(){
      this.bitmap = new hdmap.initMap({
          gisEngine: 'bitmap',
          sizeW: 1920,
          sizeH: 1080,
          domId: 'bitmap',
          mapUrl: '../src/assets/u768.jpg',
          maxZoom: 7,
          minZoom: 3,
          center: this.input,
          popupDom: {
            popup: 'popup',
            popupcloser: 'popup-closer',
            popupcontent: 'popup-content'
          }
      })
    }
    
  })
</script>

</html>

```html
<html lang="en">

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
  <link href="../src/hdmap/hdmap.css" rel="stylesheet" type="text/css" />
  <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
  <script src="../src/vue/vue.js"></script>  
  <script src="https://unpkg.com/element-ui/lib/index.js"></script>
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
  <style>
   .row{
      margin-top:4px;
    }
  </style>
</head>
<body>
  <div id="app">
    <div id="bitmap"></div>
    <el-row class='row'>
      <el-col :span="3">
        <el-button type="primary" @click='setCenter'>设置地图中心</el-button>
         </el-col>
      <el-col :span="8" :offset="1">
        <el-input v-model="input" placeholder="请输入坐标数组如[x,y]" ></el-input>
      </el-col>
    </el-row>
    <el-row class='row'>
      <el-col :span="3">
        <el-button type="success"  @click='getCenter'>获取地图中心</el-button>
         </el-col>
      <el-col :span="8" :offset="1">
        <el-input v-model="input1"></el-input>
      </el-col>
    </el-row>
    <el-row class='row'>
      <el-col :span="3">
        <el-button type="warning"  @click='setZoom'>设置放大等级</el-button>
         </el-col>
      <el-col :span="8" :offset="1">
        <el-input v-model="zoom" placeholder="当前地图放大等级"></el-input>
      </el-col>
    </el-row>
     <el-row class='row'>
      <el-col :span="3">
        <el-button type="danger"  @click='getZoom'>获取放大等级</el-button>
         </el-col>
      <el-col :span="8" :offset="1">
        <el-input v-model="getzoom" ></el-input>
      </el-col>
    </el-row>
  </div>

</body>

<script>
  new Vue({
    el: '#app',
    data: {
      input: '',
      input1: '',
      zoom: '',
      getzoom: ''
    },
    methods: {
      setCenter(){
        let input = JSON.parse(this.input)
        this.bitmap.setCenter(input)
      },
      getCenter(){
        this.input1 = JSON.stringify(this.bitmap.getCenter());
      },
      setZoom(){
        let zoom = JSON.parse(this.zoom)
        this.bitmap.setZoom(zoom)
      },
      getZoom(){
        this.getzoom = this.bitmap.getZoom();
      }
    },
    mounted(){
      this.bitmap = new hdmap.initMap({
          gisEngine: 'bitmap',
          sizeW: 1920,
          sizeH: 1080,
          domId: 'bitmap',
          mapUrl: '../src/assets/u768.jpg',
          maxZoom: 7,
          minZoom: 3,
          center: this.input,
          popupDom: {
            popup: 'popup',
            popupcloser: 'popup-closer',
            popupcontent: 'popup-content'
          }
      })
    }

  })
</script>

</html>
```

## changeMap

> <font color=#ff0000>待实现</font>

{color:red}待实现{color}
切换显示的地图

## resize

> <font color=#ff0000>待实现</font>

重置函数重置地图的状态

## destroy

> <font color=#00aa00>在 v0.1.0 中已实现</font>

注销函数，注销函数对象及地图上数据等信息

在离开页面时进行地图销毁，节省内存
