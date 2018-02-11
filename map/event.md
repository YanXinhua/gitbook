# 点位操作-事件处理

> 术语解读： feature
>
> 地图上的内容，点位，区域、路线都术语 feature 的一种

---

> <font color=#00aa00>v0.1.0 版本已实现注册和注销函数实现</font>

首先需要通过地图对象注册相应的操作监听，才能在地图上该事件触发时，通知应用进行相应的业务处理

## regEventListener

```javascript
/**
 * HDMap.prototype.regEventListener
 * 注册地图事件监听
 * @param {String} eventType : 事件类型(具体都有哪些类型查看ol.MapBrowserEvent)
 * @param call : 回调函数
 * @param featureType : 注册的事件类型在那些点位类型上生效
 */
HDMap.prototype.regEventListener = function(eventType, callback, featureType){...}
```

参数有三个时，时间类型和回调函数为必传函数，featureType 为可选参数。两个参数时，将会添加对 eventType 事件的监听回调。事件触发时返回点位上绑定的 feature 对象。如果该位置没有对象，则返回单机点的位置信息
|参数名称 | 是否必填 | 参数类型及范围 | 参数说明 |
| :--- | :--- | :--- | :--- |
| eventType | 是 | String: 'singleclick'、'dragstart'... | 事件类型 |
| call | 是 | Function | 回调函数 |
| featureType | 选填 | String | 注册的事件类型在那些点位类型上生效 |

eventType 可注册事件类型

`singleclick` 点击事件

`dragstart` 拖动开始事件

`dragend` 拖动结束事件

`selected` 选择事件

`cancelSelected` 取消选择事件

`pointermove` 光标移动事件监听

```javascript
//examples
/*
response: {
  {
    feature: feature.extProperties, // 事件所触发的feature对象的信息，这个信息及添加点位时传入的信息， 当没有点位时为null
    eventType: 'singleclick',  // 事件名称
    coordinate: e.coordinate   // 事件的点位信息
  }
}
*/
var callback = function(response) {
  console.log(response)
  if (response.feature) {
    // 事件触发在某个feature上
  } else {
    // 事件没有触发在feature上，进行自身逻辑处理
  }
}
```

## unRegEventListener

根据事件类型和 featureType 进行监听注销

注销时传递的 eventType 和 featureType 和注册时一致，即可注销相应的监听事件

```javascript
/**
 * HDMap.prototype.unRegEventListener
 * 注销地图上的事件监听
 * @param {String} eventType
 * @param {String} featureType
 */
 HDMap.prototype.unRegEventListener = function(eventType, featureType){...}
```

| 参数名称    | 是否必填 | 参数类型及范围                        | 参数说明                           |
| :---------- | :------- | :------------------------------------ | :--------------------------------- |
| eventType   | 是       | String: 'singleclick'、'dragstart'... | 事件类型                           |
| featureType | 选填     | String                                | 注册的事件类型在那些点位类型上生效 |

#singleclick--点击事件示例

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
    .Popup{
      position: relative;
    }
    .closePopup{
      position: absolute;
      top:-4px;
      right:5px;
      font-size: 12px;
      color: #666;
      font-weight: 900;
    }
  </style>
</head>
<body>
  <div id="app">
    <div id="bitmap"></div>
    <div id="Popup"  style="text-align:center;">
      <span class="closePopup" @click="close">x</span>
      <el-button type="text" @click="open">点击打开 Message Box</el-button>
    </div>
    <el-button type="warning" @click="clickWarn">开启告警点击事件</el-button>
    <el-button type="danger" @click="cancel">注销告警点击事件</el-button>
  </div>
</body>
<script>
  new Vue({
    el: '#app',
    data: {
      featureType:''
    },
    methods: {
      close(){
        this.bitmap.closePopup();
      },
      open() {
        this.$alert('这是一段内容', '标题名称', {
          confirmButtonText: '确定',
          callback: action => {
            this.$message({
              type: 'info',
              message: `action: ${action}`
            });
          }
        });
      },
      clickWarn() {
        this.featureType = 'warn'
        this.bitmap.regEventListener("singleclick", (e) => {
          this.bitmap.showPopup('Popup', e.coordinate)
        },this.featureType)
      },
      cancel(){
        //注销点击事件
        this.featureType = 'warn';
        this.bitmap.unRegEventListener("singleclick",this.featureType);
        this.close()
      }
    },
    mounted(){
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
       // 添加点位
      this.bitmap.addMarker({
        id: 111,
        position: [-151, 39.4375],
        markerType: 'warn',
        name: id,
        imgUrl: '../src/assets/warn.png',
        size: [38, 48]
      })
       // 添加弹框
      this.bitmap.addPopup('Popup')
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
    .Popup{
      position: relative;
    }
    .closePopup{
      position: absolute;
      top:-4px;
      right:5px;
      font-size: 12px;
     font-weight: 900;
    }
  </style>
</head>
<body>
  <div id="app">
    <div id="bitmap"></div>
     <div id="Popup"  style="text-align:center;">
     <span class="closePopup" @click="close">x</span>
      <el-button type="text" @click="open">点击打开 Message Box</el-button>
    </div>
    <el-button type="warning" @click="clickWarn">开启告警点击事件</el-button>
    <el-button type="danger" @click="cancel">注销告警点击事件</el-button>
  </div>
</body>
<script>
  new Vue({
    el: '#app',
    data: {
      featureType:''
    },
    methods: {
      close(){
        this.bitmap.closePopup();
      },
      open() {
        this.$alert('这是一段内容', '标题名称', {
          confirmButtonText: '确定',
          callback: action => {
            this.$message({
              type: 'info',
              message: `action: ${action}`
            });
          }
        });
      },
      clickWarn() {
        this.featureType = 'warn'
        this.bitmap.regEventListener("singleclick", (e) => {
          this.bitmap.showPopup('Popup', e.coordinate)
        },this.featureType)
      },
      cancel(){
        //注销点击事件
        this.featureType = 'warn';
        this.bitmap.unRegEventListener("singleclick",this.featureType);
        this.close()
      }
    },
    mounted(){
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
       // 添加点位
      this.bitmap.addMarker({
        id: 111,
        position: [-151, 39.4375],
        markerType: 'warn',
        name: id,
        imgUrl: '../src/assets/warn.png',
        size: [38, 48]
      })
       // 添加弹框
      this.bitmap.addPopup('Popup')
    }
  })
</script>

</html>
```
