# 新增区域示例

传入区域的点位列表，区域的样式设置信息

然后注册区域的事件回调等

## addArea

####新增单个区域

```javascript
/**
 * HDMap.prototype.addArea
 * 新增区域
 * @param {Object} areaInfo
 * @returns {ol.AreaFeature}
 * 区域参数示例
 * {
 *  id: '111' 区域id
 *  name: 'eastArea' 区域名称
 *  areaType: '01' 区域类型
 *  borderPoints: [[[42.5, 94.9375], [41.5, 33.9375], [151, 39.4375], [151.5, 99.4375], [68.5, 112.9375], [42.5, 93.9375]]]
 *    边界点list
 * }
 */
HDMap.prototype.addArea = function(areaInfo) {...}
```

| 参数名称 | 是否必填 | 参数类型及范围                                      | 参数说明               |
| :------- | :------- | :-------------------------------------------------- | :--------------------- |
| areaInfo | 是       | Object: {id:"",name:"",areaType:"",borderPoints:""} | id、名称、类型、边界点 |

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
  <!-- <link href="../src/hdmap/hdmap.css" rel="stylesheet" type="text/css" /> -->
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
</head>
<style>
    *{
      margin: 0;
      padding :0;
    }
    .popuptext {
      width: 200px;
      background: white;
      font-size: 14px;
      text-align: center;
      color: #333;
      border-radius: 10px;
      position: relative;
      left: -30px;
      top: -30px;
    }
    .popuptext span{
        width:0;
        height:0;
        border-left:20px solid transparent;
        border-right:20px solid transparent;
        border-top:20px solid #fff;
        position: absolute;
        top: 10px;
        left: 10px;
    }
</style>
  <!-- 弹框显示的内容 -->
   <div id="Popup" class="popuptext">
      <p>this is hdmap</p>
      <span></span>
   </div>
<div>
	<div id="map" style="width: 100%; height:300px">
    <div id="popup" class="ol-popup">
        <a href="#" id="popup-closer" class="ol-popup-closer"></a>
        <div id="popup-content"></div>
    </div>
</div>
    <script>
        let map = new hdmap.initMap({
            gisEngine:'bitmap',
            domId:'map',
            mapUrl:'../src/assets/map.png',
            sizeW: 1024,
            sizeH: 968,
            center:[110.619942, 25.304629],
            popupDom:{popup:'popup',
            popupcloser:'popup-closer',
            popupcontent:'popup-content'
            },
            scale: 300,
        })
        let polyCoords = [
            [
              [45.5, 94.9375],
              [41.5, 33.9375],
              [151, 39.4375],
              [151.5, 99.4375],
              [68.5, 112.9375],
              [42.5, 93.9375]
             ]
        ];
        let areaInfo = {
          id: 888008,
          name: 'eastArea',
          areaType: '02',
          borderPoints: polyCoords
        }
        let id = new Date().valueOf()
        map.addArea(areaInfo)
        //弹框设置
        let Popup = document.querySelector('#Popup');
        map.addPopup('Popup')
        map.regEventListener("singleclick", (e) => {
          //判断点位越界
          let pointArea = hdmap.utils.judgePointInsidePolygon(e.coordinate,polyCoords[0])
          if(pointArea=="on" || pointArea=="in" ){
            map.showPopup('Popup', e.coordinate)
          }
        })
        // 固定地图显示区域不受鼠标事件影响
        map.getMap().on('precompose', function() {
          map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
        })
  </script>

```html
<style>
    *{
      margin: 0;
      padding :0;
    }
    .popuptext {
      width: 200px;
      background: white;
      font-size: 14px;
      text-align: center;
      color: #333;
      border-radius: 10px;
      position: relative;
      left: -30px;
      top: -30px;
    }
    .popuptext span{
        width:0;
        height:0;
        border-left:20px solid transparent;
        border-right:20px solid transparent;
        border-top:20px solid #fff;
        position: absolute;
        top: 10px;
        left: 10px;
    }
</style>
  <!-- 弹框显示的内容 -->
   <div id="Popup" class="popuptext">
      <p>this is hdmap</p>
      <span></span>
   </div>
<div>
	<div id="map" style="width: 100%; height:300px">
    <div id="popup" class="ol-popup">
        <a href="#" id="popup-closer" class="ol-popup-closer"></a>
        <div id="popup-content"></div>
    </div>
</div>
    <script>
        let map = new hdmap.initMap({
            gisEngine:'bitmap',
            domId:'map',
            mapUrl:'../src/assets/map.png',
            sizeW: 1024,
            sizeH: 968,
            center:[110.619942, 25.304629],
            popupDom:{popup:'popup',
            popupcloser:'popup-closer',
            popupcontent:'popup-content'
            },
            scale: 300,
        })
        let polyCoords = [
            [
              [45.5, 94.9375],
              [41.5, 33.9375],
              [151, 39.4375],
              [151.5, 99.4375],
              [68.5, 112.9375],
              [42.5, 93.9375]
             ]
        ];
        let areaInfo = {
          id: 888008,
          name: 'eastArea',
          areaType: '02',
          borderPoints: polyCoords
        }
        let id = new Date().valueOf()
        map.addArea(areaInfo)
        //弹框设置
        let Popup = document.querySelector('#Popup');
        map.addPopup('Popup')
        map.regEventListener("singleclick", (e) => {
          //判断点位越界
          let pointArea = hdmap.utils.judgePointInsidePolygon(e.coordinate,polyCoords[0])
          if(pointArea=="on" || pointArea=="in" ){
            map.showPopup('Popup', e.coordinate)
          }
        })
        // 固定地图显示区域不受鼠标事件影响
        map.getMap().on('precompose', function() {
          map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
        })
  </script>
```

## addAreas

####新增多个区域

```javascript
/**
 * HDMap.prototype.addAreas
 * 批量新增区域
 * @param {Array} areaList
 */
HDMap.prototype.addAreas = function(areaList) {...}
```

| 参数名称 | 是否必填 | 参数类型及范围           | 参数说明                  |
| :------- | :------- | :----------------------- | :------------------------ |
| areaList | 是       | areaList: [{},{},{}....] | areaInfo 对象的集合成数组 |

<div>
	<div id="map2" style="width: 100%; height:300px">
    <div id="popup2" class="ol-popup">
      <a href="#" id="popup-closer2" class="ol-popup-closer"></a>
      <div id="popup-content2"></div>
    </div>
</div>
<script>
  let map2 = new hdmap.initMap({
    gisEngine:'bitmap',
    domId:'map2',
    mapUrl:'../src/assets/map.png',
    sizeW: 1024,
    sizeH: 968,
    center:[110.619942, 25.304629],
    popupDom:{popup:'popup2',popupcloser:'popup-closer2',popupcontent:'popup-content2'}
  })
   let polyCoords1 = [
      [
        [45.5, 94.9375],
        [41.5, 33.9375],
        [151, 39.4375],
        [151.5, 99.4375],
        [68.5, 112.9375],
        [42.5, 93.9375]
      ]
    ];
    let polyCoords2 = [
        [
            [-150.192114608162, 256.796067390244],
            [285.807885391838, 269.796067390244],
            [287.807885391838, 144.796067390244],
            [-49.192114608162, 137.796067390244],
            [-185.192114608162, 219.796067390244],
            [-150.192114608162, 257.796067390244]]
        ];
    let polyCoords3 = [
        [
            [-42.5, 94.9375],
            [-41.5, 33.9375],
            [-151, 39.4375],
            [-151.5, 99.4375],
            [-68.5, 112.9375],
            [-42.5, 93.9375]
        ]
      ];
    let areaInfo1 = {
        id: 111,
        name: 'eastArea',
        areaType: '01',
        borderPoints: polyCoords1
    }
    let areaInfo2 = {
        id: 112,
        name: 'eastArea',
        areaType: '02',
        borderPoints: polyCoords2
      }
    let areaInfo3 = {
        id: 113,
        name: 'eastArea',
        areaType: '03',
        borderPoints: polyCoords3
      }
    let areaList = [areaInfo1, areaInfo2, areaInfo3];
    console.log(areaList)
    let id1 = new Date().valueOf()
    map2.addAreas(areaList)
      //  固定地图显示区域不收鼠标事件影响
    for (let i = 0; i < areaList.length; i++) {
      map2.getMap().on('precompose', function () {
        map2.updateArea(areaList[i], hdmap.commonConfig.getMouseOverAreaStyle())
      })
    }
</script>

```html
<div>
	<div id="map2" style="width: 100%; height:300px">
    <div id="popup2" class="ol-popup">
      <a href="#" id="popup-closer2" class="ol-popup-closer"></a>
      <div id="popup-content2"></div>
    </div>
</div>
<script>
  let map2 = new hdmap.initMap({
    gisEngine:'bitmap',
    domId:'map2',
    mapUrl:'../src/assets/map.png',
    sizeW: 1024,
    sizeH: 968,
    center:[110.619942, 25.304629],
    popupDom:{popup:'popup2',popupcloser:'popup-closer2',popupcontent:'popup-content2'}
  })
   let polyCoords1 = [
      [
        [45.5, 94.9375],
        [41.5, 33.9375],
        [151, 39.4375],
        [151.5, 99.4375],
        [68.5, 112.9375],
        [42.5, 93.9375]
      ]
    ];
    let polyCoords2 = [
        [
            [-150.192114608162, 256.796067390244],
            [285.807885391838, 269.796067390244],
            [287.807885391838, 144.796067390244],
            [-49.192114608162, 137.796067390244],
            [-185.192114608162, 219.796067390244],
            [-150.192114608162, 257.796067390244]]
        ];
    let polyCoords3 = [
        [
            [-42.5, 94.9375],
            [-41.5, 33.9375],
            [-151, 39.4375],
            [-151.5, 99.4375],
            [-68.5, 112.9375],
            [-42.5, 93.9375]
        ]
      ];
    let areaInfo1 = {
        id: 111,
        name: 'eastArea',
        areaType: '01',
        borderPoints: polyCoords1
    }
    let areaInfo2 = {
        id: 112,
        name: 'eastArea',
        areaType: '02',
        borderPoints: polyCoords2
      }
    let areaInfo3 = {
        id: 113,
        name: 'eastArea',
        areaType: '03',
        borderPoints: polyCoords3
      }
    let areaList = [areaInfo1, areaInfo2, areaInfo3];
    console.log(areaList)
    let id1 = new Date().valueOf()
    map2.addAreas(areaList)
      //  固定地图显示区域不收鼠标事件影响
    for (let i = 0; i < areaList.length; i++) {
      map2.getMap().on('precompose', function () {
        map2.updateArea(areaList[i], hdmap.commonConfig.getMouseOverAreaStyle())
      })
    }
</script>
```
