# 新增点位

需要调用地图服务的获取点位接口，获取到当前地图上的点位信息列表，，从点位表中获取点位信息，然后通过 addMarker 方法进行新增

## addMarker

`参数`：点位对象

示例

```javascript
/**
 * 在地图上添加设备点位
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
```

需要包括点位的 id，设备类型，设备 id 等信息

## addMarkerByGPS

`参数`：GPS 信息，设备类型

`可选`：样式类型

通过 GPS 信息新增点位

地图引擎会判断当前的地图是否支持 GPS 信息的处理显示，如果是有 GPS 相对信息的地图，则转换成相应的点位进行显示

## addMarkers

`参数`：markerList 

```javascript
/**
 * 批量新增点位函数，可以处理批量点位列表
 * @param {Array} markerList
 */
```

批量添加点位
