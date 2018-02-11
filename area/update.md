# 修改区域样式

## updateArea

传入区域的 id 和样式对象

更新对应区域的样式显示

```javascript
/**
 * HDMap.prototype.updateArea
 * 更新区域样式
 * @param {Object} areaInfo
 * @param {Object} styleObject 自定义样式对象
 * styleObject 是调用函数getMouseOverAreaStyle()之后返回的对象
 */
 HDMap.prototype.updateArea = function(areaInfo, styleObject){...}
```

| 参数名称    | 是否必填 | 参数类型及范围                                      | 参数说明                                   |
| :---------- | :------- | :-------------------------------------------------- | :----------------------------------------- |
| areaInfo    | 是       | Object: {id:"",name:"",areaType:"",borderPoints:""} | id、名称、类型、边界点                     |
| styleObject | 是       | Object: {}                                          | 调用函数 getMouseOverAreaStyle()返回的对象 |

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
	<script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
</head>
<div>
  <button class="btnRed">传入红色填充</button>
  <button class="btnBlue">传入蓝色填充</button>
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
        // 固定地图显示区域不受鼠标事件影响
        map.getMap().on('precompose', function() {
          map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
        })
        let styleObject1 = {
          fillColor: "red",   
          strokeColor: "black", 
          strokeWidth: 2 
        }
        let styleObject2 = {
          fillColor: "blue",   
          strokeColor: "black", 
          strokeWidth: 2 
        }
        let btnRed = document.querySelector('.btnRed');
        let btnBlue = document.querySelector('.btnBlue');
        btnRed.onclick = function(){       
          map.getMap().on('precompose', function() {
              map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle(styleObject1))
          })
        }
        btnBlue.onclick = function(){       
          map.getMap().on('precompose', function() {
              map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle(styleObject2))
          })
        }
  </script>

```html
<div>
  <button class="btnRed">传入红色填充</button>
  <button class="btnBlue">传入蓝色填充</button>
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
        // 固定地图显示区域不受鼠标事件影响
        map.getMap().on('precompose', function() {
          map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle())
        })
        let styleObject1 = {
          fillColor: "red",
          strokeColor: "black",
          strokeWidth: 2
        }
        let styleObject2 = {
          fillColor: "blue",
          strokeColor: "black",
          strokeWidth: 2
        }
        let btnRed = document.querySelector('.btnRed');
        let btnBlue = document.querySelector('.btnBlue');
        btnRed.onclick = function(){
          map.getMap().on('precompose', function() {
              map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle(styleObject1))
          })
        }
        btnBlue.onclick = function(){
          map.getMap().on('precompose', function() {
              map.updateArea(areaInfo, hdmap.commonConfig.getMouseOverAreaStyle(styleObject2))
          })
        }
  </script>
```
