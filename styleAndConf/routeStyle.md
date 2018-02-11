#巡更样式

## getNormalRouteStyle

```javascript
/**
 * 获取巡更路线正常样式
 * @return {Object} 巡更路线正常样式对象
 */
 var getNormalRouteStyle = function getNormalRouteStyle (){...}
```

## getOfflineRouteStyle

```javascript
  /**
   * 获取巡更路线离线样式
   * @return {Object} 巡更路线离线样式对象
   */
 var getOfflineRouteStyle = function getOfflineRouteStyle (){...}
```

## getWarningRouteStyle

```javascript
 /**
   * 获取巡更路线报警样式
   * @return {Object} 巡更路线报警样式对象
   */
 var getWarningRouteStyle = function getWarningRouteStyle (){...}
```

## getRouteStyleAnimation

```javascript
  /**
   * 获取巡更路线报警动画样式
   * @param {Object} map 地图对象
   * @param {Object} lineInfo 线路参数
   * 线路参数示例
   * {
   *  id: '111' 线路id
   *  name: '巡更路线' 线路名称
   *  lineType: '01' 线路类型
   *  borderPoints: [[42.5, 94.9375], [41.5, 33.9375]......]
   * }
   */
 var getRouteStyleAnimation = function getRouteStyleAnimation (map, lineInfo){...}
```
## warnRouteCancel

```javascript
/**
   * 消除巡更路线报警动画样式
   * @param {Object} map 地图对象
   * @param {Object} lineInfo 线路参数
   * 线路参数示例
   * {
   *  id: '111' 线路id
   *  name: '巡更路线' 线路名称
   *  lineType: '01' 线路类型
   *  borderPoints: [[42.5, 94.9375], [41.5, 33.9375]......]
   * }
   */
   var warnRouteCancel = function warnRouteCancel (map, lineInfo){...}
```