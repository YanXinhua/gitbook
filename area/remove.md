# 删除和隐藏区域

## removeArea

传入区域的 id

删除地图上的区域

```javascript
/**
 * HDMap.prototype.removeArea
 * 移除区域信息
 * @param {Object} areaInfo
 */
HDMap.prototype.removeArea = function(areaInfo) {...}
```

| 参数名称 | 是否必填 | 参数类型及范围                                      | 参数说明               |
| :------- | :------- | :-------------------------------------------------- | :--------------------- |
| areaInfo | 是       | Object: {id:"",name:"",areaType:"",borderPoints:""} | id、名称、类型、边界点 |

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
</head>
<button class="removeArea">删除区域</button>
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
        // 固定地图显示区域不受鼠标事件影响
        map.getMap().on('precompose', function() {
          map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
        })
        let removeArea = document.querySelector('.removeArea');
        removeArea.onclick = function(){
          console.log(111111);
          map.removeArea(areaInfo);
        }
  </script>

```html
<button class="removeArea">删除区域</button>
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
      // 固定地图显示区域不受鼠标事件影响
      map.getMap().on('precompose', function() {
        map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
      })
      let removeArea = document.querySelector('.removeArea');
      removeArea.onclick = function(){
        console.log(111111);
        map.removeArea(areaInfo);
      }
</script>
```

## hideArea

```javascript
/**
 * HDMap.prototype.hideArea
 * 隐藏区域
 * @param {Object} areaInfo
 */
HDMap.prototype.hideArea = function(areaInfo) {...}
```

| 参数名称 | 是否必填 | 参数类型及范围                                      | 参数说明               |
| :------- | :------- | :-------------------------------------------------- | :--------------------- |
| areaInfo | 是       | Object: {id:"",name:"",areaType:"",borderPoints:""} | id、名称、类型、边界点 |

传入区域的 id

隐藏地图上对应的区域

<button class="hideArea">隐藏区域</button>
<div>
	<div id="map2" style="width: 100%; height:300px">
    <div id="popup2" class="ol-popup">
      <a href="#" id="popup-closer2" class="ol-popup-closer"></a>
      <div id="popup-content2"></div>
    </div>
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
    let areaInfo1 = {
        id: 888009,
        name: 'eastArea1',
        areaType: '02',
        borderPoints: polyCoords1
    }
    let id1 = new Date().valueOf()
    map2.addArea(areaInfo1)
     //初始化显示区域
     map2.updateArea(areaInfo1, hdmap.commonConfig.getMouseOverAreaStyle())
     let hideArea = document.querySelector('.hideArea');
     console.log(hideArea);
     hideArea.onclick = function(){
        map2.hideArea(areaInfo1);
     }
</script>

```html
<button class="hideArea">隐藏区域</button>
<div>
	<div id="map2" style="width: 100%; height:300px">
    <div id="popup2" class="ol-popup">
      <a href="#" id="popup-closer2" class="ol-popup-closer"></a>
      <div id="popup-content2"></div>
    </div>
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
    let areaInfo1 = {
        id: 888009,
        name: 'eastArea1',
        areaType: '02',
        borderPoints: polyCoords1
    }
    let id1 = new Date().valueOf()
    map2.addArea(areaInfo1)
     //初始化显示区域
     map2.updateArea(areaInfo1, hdmap.commonConfig.getMouseOverAreaStyle())
     let hideArea = document.querySelector('.hideArea');
     console.log(hideArea);
     hideArea.onclick = function(){
        map2.hideArea(areaInfo1);
     }
</script>
```
