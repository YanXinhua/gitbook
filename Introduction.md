# 简介

地图引擎hdmap是使用openlayers 3.20版本封装出的一套js类库，暴露了一系列web API供恒大智慧小区项目使用。

应用可以通过地图引擎API处理GIS地图和光栅图，可以实现地图的显示和缩放移动等地图操作。应用也可以在地图上实现点位管理、路线绘制和区域描边等功能，以实现各个小区管理、停车场、门禁、巡更等场景的业务需求。

地图引擎会在系统应用的主框架处引入。在引入地图引擎后，会在全局对象上存在一个hdmap对象，在hdmap上包含了地图的初始化函数initMap，地图管理器mapManager，地图默认样式集mapCommonConfig，地图工具函数集utils等属性。

# 引入使用

首先需要在工程的package.json中的依赖处引入

```javascript
  "dependencies": {
    ···
    "hdmap": "git+http://gitlab/xiaxuanyin/UI-mapcomponent.git#master"
    ···
  },
```

然后通过npm安装依赖

其次要在工程入口文件处引入hdmap和css文件

```javascript
import 'hdmap'
import 'hdmap/dist/hdmap.css'
```

及存在全局的hdmap对象，使用方法请看[初始化](map/init.md)

# 版本控制及更新

当我们发布版本时，开发使用者只需要在项目中运行
```javascript
npm update
```
即可更新hdmap版本。如有问题需要制定版本时，请将依赖中的master改为指定版本即可。

我们的版本更新会在开发群同步给大家，如有问题，可以到[仓库问题](http://gitlab/xiaxuanyin/UI-mapcomponent/issues)处反馈，或者按照接下来项目问题管理的流程提出。