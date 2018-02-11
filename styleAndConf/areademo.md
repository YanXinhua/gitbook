# 区域示例

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
      <h4>区域样式</h4>
      <button id="defaultAreaw" @click="addarea">添加区域</button>
      <button id="successAreaw" @click="addareaDefault">成功</button>
      <button id="addAreaw" @click="addareaWarn">报警</button>
      <button id="addAreaw" @click="closeWarn">解除警报</button>
    </div>
  </div>
  <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
        areaTest: {
          id: 222,
          name: 'testArea',
          areaType: '02',
          borderPoints: [
            [
              [-42.5, 94.9375],
              [-41.5, 33.9375],
              [-151, 39.4375],
              [-151.5, 99.4375],
              [-68.5, 112.9375],
              [-42.5, 93.9375]
            ]
          ]
        },
        radius: 0,
        flag: true
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
        // 添加区域
        addarea() {
          this.bitmap.addArea(this.areaTest)
        },
        // 区域默认样式
        addareaDefault() {
          this.bitmap.updateArea(
            this.areaTest,
            hdmap.commonConfig.getMouseOverAreaStyle()
          )
        },
        // 区域报警动画
        addareaWarn() {
          this.bitmap.warnAnimation(this.areaTest)
        },
        // 解除区域报警动画
        closeWarn() {
          this.bitmap.warnCancel(this.areaTest)
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
      <h4>区域样式</h4>
      <button id="defaultAreaw" @click="addarea">添加区域</button>
      <button id="successAreaw" @click="addareaDefault">成功</button>
      <button id="addAreaw" @click="addareaWarn">报警</button>
      <button id="addAreaw" @click="closeWarn">解除警报</button>
    </div>
  </div>
  <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
        areaTest: {
          id: 222,
          name: 'testArea',
          areaType: '02',
          borderPoints: [
            [
              [-42.5, 94.9375],
              [-41.5, 33.9375],
              [-151, 39.4375],
              [-151.5, 99.4375],
              [-68.5, 112.9375],
              [-42.5, 93.9375]
            ]
          ]
        },
        radius: 0,
        flag: true
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
        // 添加区域
        addarea() {
          this.bitmap.addArea(this.areaTest)
        },
        // 区域默认样式
        addareaDefault() {
          this.bitmap.updateArea(
            this.areaTest,
            hdmap.commonConfig.getMouseOverAreaStyle()
          )
        },
        // 区域报警动画
        addareaWarn() {
          this.bitmap.warnAnimation(this.areaTest)
        },
        // 解除区域报警动画
        closeWarn() {
          this.bitmap.warnCancel(this.areaTest)
        }
      }
    })
    </script>
</div>
```