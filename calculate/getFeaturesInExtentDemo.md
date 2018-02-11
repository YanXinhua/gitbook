#点位聚合

## getFeaturesInExtent

```javascript
/**
 * 获取点位聚合信息
 * @param {Object} map 初始化地图对象
 * @param {Array} coordinate 鼠标点击坐标，格式：[X坐标, Y坐标]
 * @param {Number} radius   区域半径
 * @return {Array} markersInfo 点位信息数组[{},{}....]
 */
function getFeaturesInExtent (map, coordinate, radius){...}
```

##注意：radius 是根据地图层级 zoom 的放大来做合理的缩小，规律为 radius / Math.pow(2, zoom - 3)(zoom>=3)

| 参数名称   | 是否必填 | 参数类型及范围       | 参数说明       |
| :--------- | :------- | :------------------- | :------------- |
| map        | 是       | Object: {}           | 初始化地图对象 |
| coordinate | 是       | Array: [x,y]         | 鼠标点击坐标   |
| radius     | 是       | Number: 1,2,3,4....n | 区域半径       |

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
    #app{
      position: relative
    }
    .container {
      position: absolute;
      right: 25px;
      top: 20px;
      background-color: #ccc;
      border-radius: 5px;
      width: 150px;
    }
    .container li{
      height: 30px;
      border-bottom: 1px solid #000;
    }
    .row{
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div id="app">
    <div id="bitmap"></div>
    <ul class="container">
      <li v-for="item in resdata" v-text="item.name"></li>
    </ul>
    <el-row class="row">
      <el-col :span="6">
        <el-button type="success" @click="getZoom">获取地图层级（最小为3）</el-button>
      </el-col>
      <el-col :span="13" :offset="2">
        <el-input v-model="zoom"></el-input>
      </el-col>
    </el-row>
    <el-row class="row">
      <el-col :span="6">
        <el-button type="success" @click ="getRadius">根据层级获取点位聚合半径</el-button>
      </el-col>
      <el-col :span="13" :offset="2">
        <el-input v-model="radius"></el-input>
      </el-col>
    </el-row>
    <hr/>
    <el-button type="primary" @click="open">开启点位聚合</el-button>
    <el-button type="success" round @click="addMarker">添加点位</el-button>
  </div>
</body>

<script>
  new Vue({
    el: '#app',
    data: {
      polyCoords: [
        [
          [-42.5, 94.9375],
          [-41.5, 33.9375],
          [-151, 39.4375],
          [-151.5, 99.4375],
          [-68.5, 112.9375],
          [-42.5, 93.9375]
        ]
      ],
      resdata: [],
      zoom:'',
      radius:''
    },
    methods: {
      open() {
        this.bitmap.regEventListener('singleclick', (e) => {
          var coordinate = e.coordinate;
          this.resdata = hdmap.utils.getFeaturesInExtent(this.bitmap, coordinate)
        });
      },
      addMarker() {
        this.bitmap.regEventListener('singleclick', (e) => {
          let id1 = new Date().valueOf()
          var coordinate = e.coordinate;
          this.bitmap.addMarker({
            id: id1,
            position: coordinate,
            markerType: 'cleaner',
            name: "清洁工4444",
            imgUrl: '../src/assets/broadcast.png',
            size: [38, 48]
          })
        });
      },
      getZoom(){
         this.zoom = this.bitmap.getZoom()
      },
      getRadius(){
        this.radius = 24 / Math.pow(2, this.zoom - 3)
      }
    },
    mounted(){
      // 初始化地图
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
      // 添加区域
      var areaInfo = {
        id: 1133333,
        name: 'eastArea',
        areaType: '01',
        borderPoints: this.polyCoords
      }
      this.bitmap.addArea(areaInfo)
       // 添加点位
      let id = new Date().valueOf()
      console.log(id);
      this.bitmap.addMarker({
        id: 111,
        position: [-34, 3.75],
        markerType: 'video',
        name: "广播",
        imgUrl: '../src/assets/broadcast.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 112,
        position: [40, 3.75],
        markerType: 'camera',
        name: "摄像头",
        imgUrl: '../src/assets/icon.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 113,
        position: [140, 43.75],
        markerType: 'guarder',
        name: "报警",
        imgUrl: '../src/assets/guard.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 114,
        position: [-140, 43.75],
        markerType: 'guarder',
        name: "报警222",
        imgUrl: '../src/assets/guard.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 115,
        position: [-190, 43.75],
        markerType: 'cleaner',
        name: "清洁工",
        imgUrl: '../src/assets/warn.png',
        size: [38, 48]
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
    #app{
      position: relative
    }
    .container {
      position: absolute;
      right: 25px;
      top: 20px;
      background-color: #ccc;
      border-radius: 5px;
      width: 150px;
    }
    .container li{
      height: 30px;
      border-bottom: 1px solid #000;
    }
    .row{
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div id="app">
    <div id="bitmap"></div>
    <ul class="container">
      <li v-for="item in resdata" v-text="item.name"></li>
    </ul>
    <el-row class="row">
      <el-col :span="6">
        <el-button type="success" @click="getZoom">获取地图层级（最小为3）</el-button>
      </el-col>
      <el-col :span="13" :offset="2">
        <el-input v-model="zoom"></el-input>
      </el-col>
    </el-row>
    <el-row class="row">
      <el-col :span="6">
        <el-button type="success" @click ="getRadius">根据层级获取点位聚合半径</el-button>
      </el-col>
      <el-col :span="13" :offset="2">
        <el-input v-model="radius"></el-input>
      </el-col>
    </el-row>
    <hr/>
    <el-button type="primary" @click="open">开启点位聚合</el-button>
    <el-button type="success" round @click="addMarker">添加点位</el-button>
  </div>
</body>

<script>
  new Vue({
    el: '#app',
    data: {
      polyCoords: [
        [
          [-42.5, 94.9375],
          [-41.5, 33.9375],
          [-151, 39.4375],
          [-151.5, 99.4375],
          [-68.5, 112.9375],
          [-42.5, 93.9375]
        ]
      ],
      resdata: [],
      zoom:'',
      radius:''
    },
    methods: {
      open() {
        this.bitmap.regEventListener('singleclick', (e) => {
          var coordinate = e.coordinate;
          this.resdata = hdmap.utils.getFeaturesInExtent(this.bitmap, coordinate)
        });
      },
      addMarker() {
        this.bitmap.regEventListener('singleclick', (e) => {
          let id1 = new Date().valueOf()
          var coordinate = e.coordinate;
          this.bitmap.addMarker({
            id: id1,
            position: coordinate,
            markerType: 'cleaner',
            name: "清洁工4444",
            imgUrl: '../src/assets/broadcast.png',
            size: [38, 48]
          })
        });
      },
      getZoom(){
         this.zoom = this.bitmap.getZoom()
      },
      getRadius(){
        this.radius = 24 / Math.pow(2, this.zoom - 3)
      }
    },
    mounted(){
      // 初始化地图
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
      // 添加区域
      var areaInfo = {
        id: 1133333,
        name: 'eastArea',
        areaType: '01',
        borderPoints: this.polyCoords
      }
      this.bitmap.addArea(areaInfo)
       // 添加点位
      let id = new Date().valueOf()
      console.log(id);
      this.bitmap.addMarker({
        id: 111,
        position: [-34, 3.75],
        markerType: 'video',
        name: "广播",
        imgUrl: '../src/assets/broadcast.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 112,
        position: [40, 3.75],
        markerType: 'camera',
        name: "摄像头",
        imgUrl: '../src/assets/icon.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 113,
        position: [140, 43.75],
        markerType: 'guarder',
        name: "报警",
        imgUrl: '../src/assets/guard.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 114,
        position: [-140, 43.75],
        markerType: 'guarder',
        name: "报警222",
        imgUrl: '../src/assets/guard.png',
        size: [38, 48]
      })
      this.bitmap.addMarker({
        id: 115,
        position: [-190, 43.75],
        markerType: 'cleaner',
        name: "清洁工",
        imgUrl: '../src/assets/warn.png',
        size: [38, 48]
      })
    }

  })
</script>

</html>
```
