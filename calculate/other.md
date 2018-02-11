#获取规则多边形的中心

## getGeometryCenter

```javascript
/**
 * 获取规则多边形的中心
 * @param {Array} points 多边形的顶点坐标：[[x1,y1],[x2,y2].....]
 * @return {Array} geometryCenter  多边形的中心(重心)：[x,y]
 */
 function getGeometryCenter (points){...}
```

#根据车位中心获取车位顶点坐标

##getParkingCoordinates

```javascript
/**
 * 根据车位中心获取车位顶点坐标
 * @param {Array} parkingCenter 车位中心坐标：[x1,y1]
 * @return {Array} borderPoints 车位顶点坐标 ：[[[x1,y1],[x2,y2],[x3,y3],[x4,y4],[x5,y5]]]
 */
 function getParkingCoordinates (parkingCenter){...}
```
