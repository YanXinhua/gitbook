# 更新点位

## updateMarker

> <font color=#00aa00>在 v0.3.0 中已实现</font>

```javascript
/**
 * 更新点位
 * @param {Object} markerInfo : 点位信息,对象
 * @param {Object} styleObj : 自定义样式，选填
 * @return {feature} 返回添加的点位对象
 * 参数示例：
 *   markerInfo: {  必填
 *    id: 1,  //唯一确定的主键 (必填)
 *    markerType: 'camera' // 点位的类型，决定该点添加的图层，如果不填写，则添加到commonLayer图层上面
 *    position: [20, 30], //点位的坐标，如果添加在光栅图中，[0,0] 这种类型的数组即可，元素0为x，元素1为y
 *    markerName:new Date().valueOf(),    //点位的名字  选填
 *    imgUrl:"arrow.png",   //点位展示的图片的url，必填
 *    size:[32,32]    //图片的大小
 *  }
 *  styleObj: { 选填
 *    color: 'red' 颜色
 *    scale: '1' 缩放
 *    opacity: '1' 透明度
 *    rotation: Math.PI 弧度
 *    anchor: [0.5,0.5] 点位中心点位置偏移
 *  }
 */
  updateMarker(markerInfo,styleobj)
```
