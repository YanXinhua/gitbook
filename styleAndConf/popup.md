# 弹窗调用

## addPopup()

> <font color=#00aa00>在 v0.3.0 中已实现</font>

```javascript
/**
   * 创建弹窗
   * @param {Object} domId 弹窗id 必填
   */
addPopup(domId)
```

## showPopup()

> <font color=#00aa00>在 v0.3.0 中已实现</font>

```javascript
/**
   * 显示弹窗
   * @param {Object} domId 弹窗id 必填
   */
showPopup(domId)
```


## closePopup()

> <font color=#00aa00>在 v0.3.0 中已实现</font>

```javascript
/**
   * 关闭弹窗
   */
closePopup()
```


# 弹窗示例

```html
<!-- 弹窗调用步骤（前提：地图已初始化成功）： -->
  export default {
    data () {
      return {
        bitmap : null
      }
    },
    mounted: {
      <!-- 初始化方法详见方法 initMap() -->
      this.bitmap = new hdmap.initMap({
        gisEngine: 'bitmap',
        sizeW: 1920,
        sizeH: 1080,
        domId: 'mainMap',
        mapUrl: mainMapImg,
        maxZoom: 3,
        minZoom: 3,
        center: [112.334403, 39.8],
        popupDom: {
          popup: 'popup',
          popupcloser: 'popup-closer',
          popupcontent: 'popup-content'
        }
      })
    }
  }
  <!-- 自定义弹窗 -->
<!-- 1.html中写好弹窗，指定id -->
  <div id="broadcastPopup">样式、内容自定义</div>
<!-- 2.注册弹窗 (调用方法：addPopup(弹窗id) ) -->
  this.bitmap.addPopup('broadcastPopup')
<!-- 3.显示弹窗 （调用方法：showPopup（弹窗id, 显示位置（Array））） -->
  this.bitmap.showPopup('broadcastPopup', [20, 20])
<!-- 4.关闭弹窗 （调用方法：closePopup（）） -->
  this.bitmap.closePopup('broadcastPopup')
  <!-- 默认弹窗 -->
<!-- 调用方法：popupDefault（position（Array），innerHtml） -->
  this.bitmap.popupDefault([0,0], 'this is default popup')
<!-- 点位聚合 (调用方法：popupMultipoint(position（Array），features(Array)) ) -->
  this.bitmap.popupMultipoint([0,0], features)
```