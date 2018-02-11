# 区域样式

## getMouseOverAreaStyle()

> <font color=#00aa00>在 v0.2.0 中已实现</font>

```javascript
/**
   * 获取鼠标默认移入区域样式
   * @param {Object} styleObj 如需自定义样式，则传，参数为 color
   * @return {Object} 样式
   */
getMouseOverAreaStyle(styleObj)
```
## getWarningAreaStyle()

> <font color=#00aa00>在 v0.3.0 中已实现</font>

```javascript
/**
   * 获取区域报警样式
   * @param {String} opacity 透明度 0-1 之间
   */
getWarningAreaStyle(opacity)
```
## getCountDefaultStyle()

> <font color=#00aa00>在 v0.4.0 中已实现</font>

```javascript
/**
   * 获取统计点默认图层样式
   * @param {String} markerInfo 点位信息
   */
getCountDefaultStyle(markerInfo)
```

## getCountWarningStyle()

> <font color=#00aa00>在 v0.4.0 中已实现</font>

```javascript
/**
   * 获取统计点报警图层样式
   * @param {String} markerInfo 点位信息
   */
getCountWarningStyle(markerInfo)
```


## warnAnimation()

> <font color=#00aa00>在 v0.4.0 中已实现</font>

```javascript
/**
  * 区域警报动画（呼吸效果）
  * @param {Object} areaInfo 
  * 区域参数示例
  * {
  *  id: '111' 区域id
  *  name: 'eastArea' 区域名称
  *  areaType: '01' 区域类型
  *  borderPoints: [[[42.5, 94.9375], [41.5, 33.9375], [151, 39.4375], [151.5, 99.4375], [68.5, 112.9375], [42.5, 93.9375]]]
  * }
  */
warnAnimation(areaInfo)
```

## warnCancel()

> <font color=#00aa00>在 v0.4.0 中已实现</font>

```javascript
/**
   * 区域警报解除
   * @param {Object} areaInfo 
   */
warnCancel(areaInfo)
```