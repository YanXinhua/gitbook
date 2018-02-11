# 范围内点位选择

## openDrawShapeTool 

`参数`： 
1. type： Circle(圆) || Box（矩形） || Polygon（多边形）
2. callback : 选择完毕后的回调

打开范围选择工具

现在是打开之后返回的是画图的事件，还需要将选择的操作放到内部的处理中

callback获取的参数应当是范围内点位的id列表或者设备列表


## closeDrawShapeTool

关闭范围选择工具