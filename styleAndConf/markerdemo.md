# 点位示例

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
  	<link href="../src/hdmap/hdmap.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
  <script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
  <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css" type="text/css">
  <script type="text/javascript" src="https://unpkg.com/vue/dist/vue.js"></script>
  <script type="text/javascript" src="https://unpkg.com/element-ui/lib/index.js"></script>
  <script type="text/javascript" src="../src/jquery/jquery-3.2.1.js" charset="utf-8"></script>
</head>
<style>
  .testbtn {
    /* width: 300px; */
    margin-top: 20px;
    margin-right: 10px;
  }
</style>
<div>
  <div class="map-container" id="app">
    <div id="bitmap"></div>
    <div class="testbtn">
      <h4>点位更新样式测试</h4>
        <el-button type="primary" plain @click="addMarker">添加点位</el-button>
        <el-button type="primary" plain @click="updateMarker">更新点位</el-button>
        <el-button type="primary" plain @click="removeMarker">删除点位</el-button>
        <el-button type="primary" plain @click="addMarkers">批量添加点位</el-button>
        <el-button type="primary" plain @click="hideMarkers">隐藏点位</el-button>
        <el-button type="primary" plain @click="showMarkers">显示点位</el-button>
        <el-button type="primary" plain @click="addCountMarker">添加统计点位</el-button>
        <el-button type="primary" plain @click="hideCountMarkers">隐藏统计点位</el-button>
        <el-button type="primary" plain @click="showCountMarkers">显示统计点位</el-button>
    </div>
  </div>
  <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
      },
      mounted() {
        console.log('mounted')
        // 初始化地图
        this.bitmap = new hdmap.initMap({
          gisEngine: 'bitmap',
          sizeW: 1920,
          sizeH: 1080,
          domId: 'bitmap',
          mapUrl: '../src/assets/u768.jpg',
          maxZoom: 3,
          minZoom: 3,
          center: [112.334403, 39.8],
          popupDom: {
            popup: 'popup',
            popupcloser: 'popup-closer',
            popupcontent: 'popup-content'
          }
        })
      },
      methods: {
        addMarker() {
          this.bitmap.addMarker({
            id: 111,
            position: [30, 20],
            markerType: 'guarder',
            markerName: '222',
            imgUrl: '../src/assets/guard.png',
          })
        },
        updateMarker() {
          this.bitmap.updateMarker({
            id: 111,
            position: [100, 100],
            markerType: 'guarder',
            markerName: '222',
            imgUrl: '../src/assets/icon.png',
          })
        },
        removeMarker() {
          this.bitmap.removeMarker({
            id: 111,
            markerType: 'guarder'
          })
        },
        addMarkers() {
          this.bitmap.addMarkers([{
            id: 111,
            position: [30, 20],
            markerType: 'guarder',
            markerName: '222',
            imgUrl: '../src/assets/guard.png',
          }, {
            id: 222,
            position: [80, -80],
            markerType: 'guarder',
            markerName: '333',
            imgUrl: '../src/assets/guard.png',
          }])
        },
        hideMarkers() {
          this.bitmap.hideMarkers('guarder')
        },
        showMarkers() {
          this.bitmap.showMarkers('guarder')
        },
        addCountMarker() {
          this.bitmap.addCountMarker({
            id: 3333,
            name: 22,
            markerType: 'countCamera',
            position: [0, 10],
            url: '../src/assets/u349.png',
            baseUrl: '../src/assets/u887.png',
            cameraNum: '9' 
          })
        },
        hideCountMarkers() {
          this.bitmap.hideCountMarkers('countCamera')
        },
        showCountMarkers() {
          this.bitmap.showCountMarkers('countCamera')
        }
      }
    })
    </script>
</div>

```html
<style>
  .testbtn {
    /* width: 300px; */
    margin-top: 20px;
    margin-right: 10px;
  }
</style>
<div>
  <div class="map-container" id="app">
    <div id="bitmap"></div>
    <div class="testbtn">
      <h4>点位更新样式测试</h4>
        <el-button type="primary" plain @click="addMarker">添加点位</el-button>
        <el-button type="primary" plain @click="updateMarker">更新点位</el-button>
        <el-button type="primary" plain @click="removeMarker">删除点位</el-button>
        <el-button type="primary" plain @click="addMarkers">批量添加点位</el-button>
        <el-button type="primary" plain @click="hideMarkers">隐藏点位</el-button>
        <el-button type="primary" plain @click="showMarkers">显示点位</el-button>
        <el-button type="primary" plain @click="addCountMarker">添加统计点位</el-button>
        <el-button type="primary" plain @click="hideCountMarkers">隐藏统计点位</el-button>
        <el-button type="primary" plain @click="showCountMarkers">显示统计点位</el-button>
    </div>
  </div>
  <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
      },
      mounted() {
        console.log('mounted')
        // 初始化地图
        this.bitmap = new hdmap.initMap({
          gisEngine: 'bitmap',
          sizeW: 1920,
          sizeH: 1080,
          domId: 'bitmap',
          mapUrl: '../src/assets/u768.jpg',
          maxZoom: 3,
          minZoom: 3,
          center: [112.334403, 39.8],
          popupDom: {
            popup: 'popup',
            popupcloser: 'popup-closer',
            popupcontent: 'popup-content'
          }
        })
      },
      methods: {
        addMarker() {
          this.bitmap.addMarker({
            id: 111,
            position: [30, 20],
            markerType: 'guarder',
            markerName: '222',
            imgUrl: '../src/assets/guard.png',
          })
        },
        updateMarker() {
          this.bitmap.updateMarker({
            id: 111,
            position: [100, 100],
            markerType: 'guarder',
            markerName: '222',
            imgUrl: '../src/assets/icon.png',
          })
        },
        removeMarker() {
          this.bitmap.removeMarker({
            id: 111,
            markerType: 'guarder'
          })
        },
        addMarkers() {
          this.bitmap.addMarkers([{
            id: 111,
            position: [30, 20],
            markerType: 'guarder',
            markerName: '222',
            imgUrl: '../src/assets/guard.png',
          }, {
            id: 222,
            position: [80, -80],
            markerType: 'guarder',
            markerName: '333',
            imgUrl: '../src/assets/guard.png',
          }])
        },
        hideMarkers() {
          this.bitmap.hideMarkers('guarder')
        },
        showMarkers() {
          this.bitmap.showMarkers('guarder')
        },
        addCountMarker() {
          this.bitmap.addCountMarker({
            id: 3333,
            name: 22,
            markerType: 'countCamera',
            position: [0, 10],
            url: '../src/assets/u349.png',
            baseUrl: '../src/assets/u887.png',
            cameraNum: '9' 
          })
        },
        hideCountMarkers() {
          this.bitmap.hideCountMarkers('countCamera')
        },
        showCountMarkers() {
          this.bitmap.showCountMarkers('countCamera')
        }
      }
    })
    </script>
</div>
```
