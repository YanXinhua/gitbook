# 统计点位示例

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
    width: 300px;
    margin-top: 20px;
    margin-right: 10px;
  }
</style>
<div>
  <div class="map-container" id="app">
    <div id="bitmap"></div>
    <div class="testbtn">
      <h4>添加统计点图标</h4>
      <button id="countCamera" @click="countCamera">摄像头</button>
      <button id="countCleaner" @click="countWarn">报警</button>
      <button id="countBroadcast" @click="countBroadcast">广播</button>
    </div>
    <div class="testbtn">
      <h4>切换显示统计点图标</h4>
      <label>
        <input id="checkcamera" type="checkbox" checked="cameraflag" @click="isShowCountCamera">摄像头</label>
      <label>
        <input id="checkwarning" type="checkbox" checked="warnflag" @click="isShowCountWarn">报警</label>
      <label>
        <input id="checkbroadcast" type="checkbox" checked="broadcastflag" @click="isShowCountBroadcast">广播</label>
    </div>
  </div>
    <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
        cameraflag: true,
        warnflag: true,
        broadcastflag: true
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
        let id = new Date().valueOf()
        let that = this
      },
      methods: {
        countCamera() {
          this.bitmap.addCountMarker(
            {
              id: 22,
              name: 22,
              markerType: 'countCamera',
              position: [40, 40],
              url: '../src/assets/u349.png',
              baseUrl: '../src/assets/u887.png',
              cameraNum: '999'
            }
          )
        },
        // 添加统计报警点
        countWarn() {
          this.bitmap.addCountMarker(
            {
              id: 22,
              name: 22,
              markerType: 'countWarning',
              position: [-40, -60],
              url: '../src/assets/u787.png',
              baseUrl: '../src/assets/u1076.png',
              warnNum: '88'
            }
          )
        },
        // 添加统计广播点
        countBroadcast() {
          this.bitmap.addCountMarker(
            {
              id: 22,
              name: 22,
              markerType: 'countBroadcast',
              position: [-120, 10],
              url: '../src/assets/u950.png',
              baseUrl: '../src/assets/u887.png',
              broadcastNum: '8'
            }
          )
        },
        isShowCountCamera() {
          if (this.cameraflag) {
            this.bitmap.hideCountMarkers('countCamera')
            this.cameraflag = false
          } else {
            this.bitmap.showCountMarkers('countCamera')
            this.cameraflag = true
          }
        },
        isShowCountBroadcast() {
          if (this.broadcastflag) {
            this.bitmap.hideCountMarkers('countBroadcast')
            this.broadcastflag = false
          } else {
            this.bitmap.showCountMarkers('countBroadcast')
            this.broadcastflag = true
          }
        },
        isShowCountWarn() {
          if (this.warnflag) {
            this.bitmap.hideCountMarkers('countWarning')
            this.warnflag = false
          } else {
            this.bitmap.showCountMarkers('countWarning')
            this.warnflag = true
          }
        }
      }
    })
    </script>
</div>

```html
<style>
  .testbtn {
    width: 300px;
    margin-top: 20px;
    margin-right: 10px;
  }
</style>
<div>
  <div class="map-container" id="app">
    <div id="bitmap"></div>
    <div class="testbtn">
      <h4>添加统计点图标</h4>
      <button id="countCamera" @click="countCamera">摄像头</button>
      <button id="countCleaner" @click="countWarn">报警</button>
      <button id="countBroadcast" @click="countBroadcast">广播</button>
    </div>
    <div class="testbtn">
      <h4>切换显示统计点图标</h4>
      <label>
        <input id="checkcamera" type="checkbox" checked="cameraflag" @click="isShowCountCamera">摄像头</label>
      <label>
        <input id="checkwarning" type="checkbox" checked="warnflag" @click="isShowCountWarn">报警</label>
      <label>
        <input id="checkbroadcast" type="checkbox" checked="broadcastflag" @click="isShowCountBroadcast">广播</label>
    </div>
    <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
        cameraflag: true,
        warnflag: true,
        broadcastflag: true
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
        let id = new Date().valueOf()
        let that = this
      },
      methods: {
        // 添加统计摄像头
        countCamera() {
          this.bitmap.addCountMarker(
            {
              id: 22,
              name: 22,
              markerType: 'countCamera',
              position: [40, 40],
              url: '../src/assets/u349.png',
              baseUrl: '../src/assets/u887.png',
              cameraNum: '999'
            }
          )
        },
        // 添加统计报警点
        countWarn() {
          this.bitmap.addCountMarker(
            {
              id: 22,
              name: 22,
              markerType: 'countWarning',
              position: [-40, -60],
              url: '../src/assets/u787.png',
              baseUrl: '../src/assets/u1076.png',
              warnNum: '88'
            }
          )
        },
        // 添加统计广播点
        countBroadcast() {
          this.bitmap.addCountMarker(
            {
              id: 22,
              name: 22,
              markerType: 'countBroadcast',
              position: [-120, 10],
              url: '../src/assets/u950.png',
              baseUrl: '../src/assets/u887.png',
              broadcastNum: '8'
            }
          )
        },
        // 是否显示统计摄像头
        isShowCountCamera() {
          if (this.cameraflag) {
            this.bitmap.hideCountMarkers('countCamera')
            this.cameraflag = false
          } else {
            this.bitmap.showCountMarkers('countCamera')
            this.cameraflag = true
          }
        },
        // 是否显示统计广播点
        isShowCountBroadcast() {
          if (this.broadcastflag) {
            this.bitmap.hideCountMarkers('countBroadcast')
            this.broadcastflag = false
          } else {
            this.bitmap.showCountMarkers('countBroadcast')
            this.broadcastflag = true
          }
        },
        // 是否显示统计报警点
        isShowCountWarn() {
          if (this.warnflag) {
            this.bitmap.hideCountMarkers('countWarning')
            this.warnflag = false
          } else {
            this.bitmap.showCountMarkers('countWarning')
            this.warnflag = true
          }
        },
      }
    })
    </script>
</div>
```
