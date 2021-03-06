# Release Notes

# v0.5.0

### 更新内容

1. 算法优化

2. 优化方法入参验证

3. 区域优化

# v0.4.2

### 更新内容
1. 增加异常判断处理
2. 完善demo文档
3. 新增点位删除方法 removeMarker(markerInfo)
4. 优化更新点位传参方式 updateMarker(markerInfo, styleObj)
### 更新内容

# v0.4.1

### 更新内容

1. 对外example框架优化
2. 新增越界判断函数judgePointInsidePolygon
3. 路线处理函数实现
4. 计算函数和样式优化

# v0.4.0

### 更新内容
1. pointermove事件监听完善

2. 区域、路线编辑方法增加可编辑功能openDrawShapeTool、openDrawLineTool

3. 区域重心和广播、摄像头、报警坐标功能函数的封装以及在vue工程上面实现例子

# myopenlayers v1.1.0

升级openlayers的代码为v4.5.0，以便使用myopenlayers的区域编辑，计算方法等新特性

# v0.3.1
### Release Notes
1. 默认样式的优化
2. 实现区域的图层处理逻辑，在首次添加区域时创建gislayer
3. addArea,addAreas, updateArea, removeArea函数功能实现
4. 新增创建overlay方法： addPopup(overlayName,弹窗id)
5. 新增显示弹窗方法：showPopup(overlayName,coordinate)
6. 默认弹窗方法更改为：popupDefault(coordinate,feature,innerHTML)
7. 优化关闭弹窗方法：closePopup()
8. 新增设置地图编辑状态方法：setMapEditState(type)//type = drawLineState：画线，drawShapeState：画图，dragState：编辑点位
9. 新增获取地图编辑状态方法：getMapEditState() //编辑状态返回对应状态类型，非编辑状态返回空字符串

# v0.3.0

1. 默认弹窗以及点位聚合弹窗功能
2. 点位更新updateMarker功能
3. 点位聚合计算函数实现
4. 点位删除功能实现
5. 默认样式集中
  1. 点位报警样式
  2. 区域报警样式

# v0.2.0

1. 实现了点位新增时对图层的判断控制逻辑
2. 图层显示隐藏的控制实现(showMarkers, hideMarkers)
3. 事件处理机制完善
4. 距离计算函数，比例尺计算函数实现()

# v0.1.0
1. 重构打包流程，排除openlayers源码

2. 实现事件注册机制，在地图构建时注册默认监听，用户的监听会在默认监听中进行处理

# v0.0.2

1. 修改了对openlayers的引入使用方式，不再将其打包到hdmap.js中，因为这样会引起初始化错误
2. 修改了hdmap的main入口文件为mapManager.js文件，不使用组件本身的全包文件
3. 解决了baidu-projection对象报错问题

# v0.1.0 myopenlayers

This project provide an openlayers module that has been rebuild for hdmap.

You can import this module to hdmap, then there will be window.ol & window.goog impl to use. 

## Use
1. add the behind module to your dependecies of hdmap,
```
"myopenlayers": "git+http://gitlab/xiaxuanyin/UI-mapcomponent.git#myopenlayers"
```
2. then import myopenlayers at the code of hdmap entry file or bundle file 

## code part

我们添加了下面两行代码到原来的openlayers的代码中，这样openlayers才能够提供出全局的ol对象和goog对象用来进行扩展。
```javascript
window.ol = ol;
window.goog = goog;
```

# v0.0.1
Base version of hdmap engine.

Add the behind line to the package.json file of your project,

```
"hdmap": "git+http://gitlab/xiaxuanyin/UI-mapcomponent.git#master"
```

then import hdmap and css file at the enter file of your project file 

```
import 'hdmap'
import 'hdmap/dist/hdmap.css'
```
