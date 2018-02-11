# 弹窗示例

<head>
	<link href="../src/ol_v3.20.0/ol.css" rel="stylesheet" type="text/css" />
  	<link href="../src/hdmap/hdmap.css" rel="stylesheet" type="text/css" />
	<script type="text/javascript" src="../src/ol_v3.20.0/ol-debug.js" charset="utf-8"></script>
  <script type="text/javascript" src="../src/hdmap/hdmap.js" charset="utf-8"></script>
  <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css" type="text/css">
  <script type="text/javascript" src="https://unpkg.com/vue/dist/vue.js"></script>
  <script type="text/javascript" src="https://unpkg.com/element-ui/lib/index.js"></script>
  <script type="text/javascript" src="../src/jquery/jquery-3.2.1.js" charset="utf-8"></script>
</head>
  <style>
  .testclass {
    width: 300px;
    padding: 10px;
    background: white;
    text-align: center;
    color: red;
    border-radius: 10px;
  }
  .testbtn {
    width: 300px;
    margin-top: 20px;
    margin-right: 10px;
  }
  </style>
<div>
  <div class="map-container" id="app">
    <div id="bitmap"></div>
    <!--摄像头弹窗 -->
    <div id="camera" class="testclass">
      <el-button type="text" @click="open3">点击打开 Message Box</el-button>
    </div>
    <!-- 保安弹窗 -->
    <div id="guarder" class="testclass">
      <el-button type="text" @click="outerVisible = true">点击打开外层 Dialog</el-button>
    </div>
    <el-dialog title="外层 Dialog" :visible.sync="outerVisible">
      <el-dialog width="30%" title="内层 Dialog" :visible.sync="innerVisible" append-to-body>
      </el-dialog>
      <div slot="footer" class="dialog-footer">
        <el-button @click="outerVisible = false">取 消</el-button>
        <el-button type="primary" @click="innerVisible = true">打开内层 Dialog</el-button>
      </div>
    </el-dialog>
    <!-- 广播弹窗 -->
    <div id="broadcast" class="testclass">
      <el-radio-group v-model="labelPosition" size="small">
        <el-radio-button label="left">左对齐</el-radio-button>
        <el-radio-button label="right">右对齐</el-radio-button>
      </el-radio-group>
      <div style="margin: 20px;"></div>
      <el-form :label-position="labelPosition" label-width="80px" :model="formLabelAlign">
        <el-form-item label="名称">
          <el-input v-model="formLabelAlign.name"></el-input>
        </el-form-item>
        <el-form-item label="活动区域">
          <el-input v-model="formLabelAlign.region"></el-input>
        </el-form-item>
        <el-form-item label="活动形式">
          <el-input v-model="formLabelAlign.type"></el-input>
        </el-form-item>
      </el-form>
    </div>
    <div class="testbtn">
      <h4>弹窗</h4>
      <button id="camerapop" @click="camerapopup">摄像头</button>
      <button id="guarderpop" @click="guarderpopup">保安</button>
      <button id="guarderpop" @click="broadcastpopup">广播</button>
      <button id="morefeature" @click="mutiplepopup">聚合</button>
      <button id="closepop" @click="closepopup">关闭</button>
    </div>
  </div>
  <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
        outerVisible: false,
        innerVisible: false,
        tabPosition: 'top',
        labelPosition: 'right',
        formLabelAlign: {
          name: '',
          region: '',
          type: ''
        },
        featureList: [
          {
            extProperties: {
              markerImg: '../src/assets/u4838.png',
              markerName: '摄像头',
              markerType: 'camera'
            }
          },
          {
            extProperties: {
              markerImg: '../src/assets/u4828.png',
              markerName: '保安',
              markerType: 'guarder'
            }
          },
          {
            extProperties: {
              markerImg: '../src/assets/u4833.png',
              markerName: '广播',
              markerType: 'broadcast'
            }
          }
        ]
      },
      mounted() {
        console.log('mounted')
        // 初始化地图
        this.bitmap = new hdmap.initMap({
          gisEngine: 'bitmap',
          sizeW: 1920,
          sizeH: 1080,
          domId: 'bitmap',
          mapUrl: '../src/assets/u768.jpg',
          maxZoom: 3,
          minZoom: 3,
          center: [112.334403, 39.8],
          popupDom: {
            popup: 'popup',
            popupcloser: 'popup-closer',
            popupcontent: 'popup-content'
          }
        })
        let id = new Date().valueOf()
        // 添加摄像头点位
        this.bitmap.addMarker({
          id: 111,
          position: [30, 20],
          markerType: 'camera',
          markerName: id,
          imgUrl: '../src/assets/icon.png',
          size: [32, 48]
        })
        // 添加保安点位
        this.bitmap.addMarker({
          id: 333,
          position: [-50, 0],
          markerType: 'guarder',
          markerName: id,
          imgUrl: '../src/assets/guard.png'
        })
        // 添加广播点位
        this.bitmap.addMarker({
          id: 444,
          position: [-100, -100],
          markerType: 'broadcast',
          markerName: id,
          imgUrl: '../src/assets/broadcast.png'
        })
        let that = this
        // 添加摄像头、保安、广播弹窗
        this.bitmap.addPopup('camera')
        this.bitmap.addPopup('guarder')
        this.bitmap.addPopup('broadcast')
        // 注册单击事件（点击地图实现）
        this.bitmap.regEventListener('singleclick', function(respones) {
          if (respones.feature) {
            // 根据点击处的点位的 markertype 显示对应的弹窗
            if (respones.feature.markerType === 'camera') {
              that.bitmap.showPopup('camera', respones.coordinate)
            } else if (respones.feature.markerType === 'broadcast') {
              that.bitmap.showPopup('broadcast', respones.coordinate)
            } else if (respones.feature.markerType === 'guarder') {
              that.bitmap.showPopup('guarder', respones.coordinate)
            }
          } else {
            // 关闭弹窗
            that.bitmap.closePopup()
          }
        })
      },
      methods: {
        // 显示摄像头弹窗
        camerapopup() {
          this.bitmap.showPopup('camera', [0, 0])
        },
        // 显示保安弹窗
        guarderpopup() {
          this.bitmap.showPopup('guarder', [0, 0])
        },
        // 显示广播弹窗
        broadcastpopup() {
          this.bitmap.showPopup('broadcast', [0, -100])
        },
        // 显示聚合弹窗
        mutiplepopup() {
          this.bitmap.popupMultipoint([0, 0], this.featureList)
        },
        // 显示关闭弹窗
        closepopup() {
          this.bitmap.closePopup()
        },
        open3() {
          this.$prompt('请输入邮箱', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            inputPattern: /[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/,
            inputErrorMessage: '邮箱格式不正确'
          })
            .then(({ value }) => {
              this.$message({
                type: 'success',
                message: '你的邮箱是: ' + value
              })
            })
            .catch(() => {
              this.$message({
                type: 'info',
                message: '取消输入'
              })
            })
        }
      }
    })
    </script>
</div>

```html
  <style>
  .testclass {
    width: 300px;
    padding: 10px;
    background: white;
    text-align: center;
    color: red;
    border-radius: 10px;
  }
  .testbtn {
    width: 300px;
    margin-top: 20px;
    margin-right: 10px;
  }
  </style>
<div>
  <div class="map-container" id="app">
    <div id="bitmap"></div>
    <!--摄像头弹窗 -->
    <div id="camera" class="testclass">
      <el-button type="text" @click="open3">点击打开 Message Box</el-button>
    </div>
    <!-- 保安弹窗 -->
    <div id="guarder" class="testclass">
      <el-button type="text" @click="outerVisible = true">点击打开外层 Dialog</el-button>
    </div>
    <el-dialog title="外层 Dialog" :visible.sync="outerVisible">
      <el-dialog width="30%" title="内层 Dialog" :visible.sync="innerVisible" append-to-body>
      </el-dialog>
      <div slot="footer" class="dialog-footer">
        <el-button @click="outerVisible = false">取 消</el-button>
        <el-button type="primary" @click="innerVisible = true">打开内层 Dialog</el-button>
      </div>
    </el-dialog>
    <!-- 广播弹窗 -->
    <div id="broadcast" class="testclass">
      <el-radio-group v-model="labelPosition" size="small">
        <el-radio-button label="left">左对齐</el-radio-button>
        <el-radio-button label="right">右对齐</el-radio-button>
      </el-radio-group>
      <div style="margin: 20px;"></div>
      <el-form :label-position="labelPosition" label-width="80px" :model="formLabelAlign">
        <el-form-item label="名称">
          <el-input v-model="formLabelAlign.name"></el-input>
        </el-form-item>
        <el-form-item label="活动区域">
          <el-input v-model="formLabelAlign.region"></el-input>
        </el-form-item>
        <el-form-item label="活动形式">
          <el-input v-model="formLabelAlign.type"></el-input>
        </el-form-item>
      </el-form>
    </div>
    <div class="testbtn">
      <h4>弹窗</h4>
      <button id="camerapop" @click="camerapopup">摄像头</button>
      <button id="guarderpop" @click="guarderpopup">保安</button>
      <button id="guarderpop" @click="broadcastpopup">广播</button>
      <button id="morefeature" @click="mutiplepopup">聚合</button>
      <button id="closepop" @click="closepopup">关闭</button>
    </div>
    <script>
    var app = new Vue({
      el: '#app',
      data: {
        // eslint-disable-next-line
        overlay: new ol.Overlay({}),
        bitmap: null,
        outerVisible: false,
        innerVisible: false,
        tabPosition: 'top',
        labelPosition: 'right',
        formLabelAlign: {
          name: '',
          region: '',
          type: ''
        },
        featureList: [
          {
            extProperties: {
              markerImg: '../src/assets/u4838.png',
              markerName: '摄像头',
              markerType: 'camera'
            }
          },
          {
            extProperties: {
              markerImg: '../src/assets/u4828.png',
              markerName: '保安',
              markerType: 'guarder'
            }
          },
          {
            extProperties: {
              markerImg: '../src/assets/u4833.png',
              markerName: '广播',
              markerType: 'broadcast'
            }
          }
        ]
      },
      mounted() {
        console.log('mounted')
        // 初始化底图
        this.bitmap = new hdmap.initMap({
          gisEngine: 'bitmap',
          sizeW: 1920,
          sizeH: 1080,
          domId: 'bitmap',
          mapUrl: '../src/assets/u768.jpg',
          maxZoom: 3,
          minZoom: 3,
          center: [112.334403, 39.8],
          popupDom: {
            popup: 'popup',
            popupcloser: 'popup-closer',
            popupcontent: 'popup-content'
          }
        })
        let id = new Date().valueOf()
        // 添加摄像头点位
        this.bitmap.addMarker({
          id: 111,
          position: [30, 20],
          markerType: 'camera',
          markerName: id,
          imgUrl: '../src/assets/icon.png',
          size: [32, 48]
        })
        // 添加保安点位
        this.bitmap.addMarker({
          id: 333,
          position: [-50, 0],
          markerType: 'guarder',
          markerName: id,
          imgUrl: '../src/assets/guard.png'
        })
        // 添加广播点位
        this.bitmap.addMarker({
          id: 444,
          position: [-100, -100],
          markerType: 'broadcast',
          markerName: id,
          imgUrl: '../src/assets/broadcast.png'
        })
        let that = this
        // 添加摄像头、保安、广播弹窗
        this.bitmap.addPopup('camera')
        this.bitmap.addPopup('guarder')
        this.bitmap.addPopup('broadcast')
        // 注册单击事件（点击地图实现）
        this.bitmap.regEventListener('singleclick', function(respones) {
          if (respones.feature) {
            // 根据点击处的点位的 markertype 显示对应的弹窗
            if (respones.feature.markerType === 'camera') {
              that.bitmap.showPopup('camera', respones.coordinate)
            } else if (respones.feature.markerType === 'broadcast') {
              that.bitmap.showPopup('broadcast', respones.coordinate)
            } else if (respones.feature.markerType === 'guarder') {
              that.bitmap.showPopup('guarder', respones.coordinate)
            }
          } else {
            // 关闭弹窗
            that.bitmap.closePopup()
          }
        })
      },
      methods: {
        // 显示摄像头弹窗
        camerapopup() {
          this.bitmap.showPopup('camera', [0, 0])
        },
        // 显示保安弹窗
        guarderpopup() {
          this.bitmap.showPopup('guarder', [0, 0])
        },
        // 显示广播弹窗
        broadcastpopup() {
          this.bitmap.showPopup('broadcast', [0, -100])
        },
        // 显示聚合弹窗
        mutiplepopup() {
          this.bitmap.popupMultipoint([0, 0], this.featureList)
        },
        // 显示关闭弹窗
        closepopup() {
          this.bitmap.closePopup()
        },
        open3() {
          this.$prompt('请输入邮箱', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            inputPattern: /[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/,
            inputErrorMessage: '邮箱格式不正确'
          })
            .then(({ value }) => {
              this.$message({
                type: 'success',
                message: '你的邮箱是: ' + value
              })
            })
            .catch(() => {
              this.$message({
                type: 'info',
                message: '取消输入'
              })
            })
        }
      }
    })
    </script>
  </div>
```