# uni-app

## 目录结构

```
┌─uniCloud              云空间目录，阿里云为uniCloud-aliyun,腾讯云为uniCloud-tcb（详见uniCloud）
│─components            符合vue组件规范的uni-app组件目录
│  └─comp-a.vue         可复用的a组件
├─utssdk                存放uts文件
├─pages                 业务页面文件存放的目录
│  ├─index
│  │  └─index.vue       index页面
│  └─list
│     └─list.vue        list页面
├─static                存放应用引用的本地静态资源（如图片、视频等）的目录，注意：静态资源只能存放于此
├─uni_modules           存放[uni_module](/uni_modules)。
├─platforms             存放各平台专用页面的目录，详见
├─nativeplugins         App原生语言插件 详见
├─nativeResources       App端原生资源目录
│  └─android            Android原生资源目录 详见
├─hybrid                App端存放本地html文件的目录，详见
├─wxcomponents          存放小程序组件的目录，详见
├─unpackage             非工程代码，一般存放运行或发行的编译结果
├─AndroidManifest.xml   Android原生应用清单文件 详见
├─main.js               Vue初始化入口文件
├─App.vue               应用配置，用来配置App全局样式以及监听 应用生命周期
├─manifest.json         配置应用名称、appid、logo、版本等打包信息，详见
├─pages.json            配置页面路由、导航条、选项卡等页面类信息，详见
└─uni.scss              这里是uni-app内置的常用样式变量
```

## pages

- 每个页面都需要在pages.json文件中配置

- 配置格式如下：

  ```json
  "pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
      {
          "path": "pages/index/index",
          "style": {
              "navigationBarTitleText": "主页",
              "navigationBarTextStyle": "white",
              "navigationBarBackgroundColor": "#28A745"
          }
      },
      {
          "path": "pages/news/news",
          "style": { ... }
      }
  ]
  ```

- 其中path为页面路径，style为页面窗口表现，常用属性包括：

  - navigationBarTitleText：导航栏标题文字内容

  - navigationBarBackgroundColor：导航栏背景颜色

  - navigationBarTextStyle：导航栏标题颜色及状态栏前景颜色，仅支持 black/white

## 底部导航tabBar

- 需要在pages.json文件中配置

- 配置格式如下：

  ```json
  "tabBar": {
      "color": "#7A7E83",
      "selectedColor": "#3cc51f",
      "backgroundColor": "#FFFFFF",
      "list": [{
              "pagePath": "pages/index/index",
              "text": "主页"
          },
          {
              "pagePath": "pages/news/news",
              "text": "新闻"
          }
      ]
  },
  ```

- 常用属性：

  color（必填）：文字默认颜色

  selectedColor（必填）：文字选中时颜色

  backgroundColor（必填）：背景颜色

  list（必填）：tab 的列表，接收一个数组，数组中的每个项都是一个对象，常用属性值如下：

  - pagePath（必填）：页面路径，必须在 pages 中先定义
  - text（必填）：tab 上按钮文字
  - iconPath：图片路径，icon 大小限制为40kb，建议尺寸为 81px * 81px，当 position 为 top 时，此参数无效，不支持网络图片，不支持字体图标
  - selectedIconPath：选中时的图片路径，icon 大小限制为40kb，建议尺寸为 81px * 81px ，当 position 为 top 时，此参数无效
  - visible：是否显示
  - iconfont：字体图标，优先级高于 iconPath

  fontSize：文字默认大小

  iconWidth：图标默认宽度（高度等比例缩放）

  spacing：图标和文字的间距

  height：tabBar 默认高度

## 页面跳转

使用navigator标签跳转：

- `<navigator url="detail">新闻详情页面</navigator>`

- 常用属性：

  url：应用内的跳转链接，值为相对路径或绝对路径，如："../first/first"，"/pages/first/first"，注意不能加 `.vue` 后缀

  open-type：跳转方式，默认值navigate

  - 跳转tabbar页面，必须设置open-type="switchTab"

  hover-class：指定点击时的样式类，当hover-class="none"时，没有点击态效果、

- 

[使用API：](https://uniapp.dcloud.net.cn/api/router.html#)

- uni.navigateTo(OBJECT)

  保留当前页面，跳转到应用内的某个页面，使用`uni.navigateBack`可以返回到原页面

  参数：url：需要跳转的应用内非 tabBar 的页面的路径 , 路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2'，path为下一个页面的路径，下一个页面的onLoad函数可得到传递的参数

  使用：

  ```js
  // 第一个页面
  goToDetail(){
      uni.navigateTo({ // 点击按钮后跳转detail页面，携带name参数Jack
          url:'/pages/news/detail?name=Jack'
      })
  }
  // Detail页面
  onLoad(options) { // 在onLoad中接收携带的参数
      this.name = options.name
  }
  ```

- uni.redirectTo(OBJECT)

  关闭当前页面，跳转到应用内的某个页面，其余与uni.navigateTo类似

- uni.reLaunch(OBJECT)

  关闭所有页面，打开到应用内的某个页面

- uni.switchTab(OBJECT)

  跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面

## 页面通讯

https://uniapp.dcloud.net.cn/api/window/communication.html

- uni.$emit(eventName,OBJECT)

  触发全局的自定义事件，附加参数都会传给监听器回调函数

  eventName：事件名

  OBJECT：触发事件携带的附加参数

  `uni.$emit('update',{msg:'页面更新'})`

- uni.$on(eventName,callback)

  监听全局的自定义事件，事件由 `uni.$emit` 触发，回调函数会接收事件触发函数的传入参数

  eventName：事件名
  callback：事件的回调函数
  
  ```js
  uni.$on('update',function(data){
      console.log('监听到事件来自 update ，携带参数 msg 为：' + data.msg);
  })
  ```
  
- uni.$once(eventName,callback)

  监听全局的自定义事件，事件由 `uni.$emit` 触发，但仅触发一次，在第一次触发之后移除该监听器。

  eventName：事件名
  callback：事件的回调函数

  ```js
  uni.$once('update',function(data){
      console.log('监听到事件来自 update ，携带参数 msg 为：' + data.msg);
  })
  ```

- uni.$off([eventName, callback])

  移除全局自定义事件监听器

  - 如果uni.$off没有传入参数，则移除App级别的所有事件监听器
  - 如果只提供了事件名（eventName），则移除该事件名对应的所有监听器
  - 如果同时提供了事件与回调，则只移除这个事件回调的监听器
  - 提供的回调必须跟$on的回调为同一个才能移除这个回调的监听器

- **注意事项**

  - uni.$emit、 uni.$on 、 uni.$once 、uni.$off 触发的事件都是 App 全局级别的，跨任意组件，页面，nvue，vue 等
  - 使用时，注意及时销毁事件监听，比如，页面 onLoad 里边 uni.$on 注册监听，onUnload 里边 uni.$off 移除，或者一次性的事件，直接使用 uni.$once 监听
  - 注意 uni.$on 定义完成后才能接收到 uni.$emit 传递的数据

## 网络

- [uni.request(OBJECT)](https://uniapp.dcloud.net.cn/api/request/request.html)

  发起网络请求

  Object常用参数：

  - url：开发者服务器接口地址
  - data：请求的参数
  - header：请求头
  - method：默认GET，支持GET,POST,PUT,DELETE,CONNECT,HEAD,OPTIONS,TRACE
  - timeout：超时时间，单位毫秒，默认60000
  - success：调用成功回调函数
  - fail：调用失败回调函数
  - complete：调用结束回调函数，是否成功都会回调

  ```js
  uni.request({
      url: 'https://www.example.com/request',
      method: 'GET',
      data: {
          text: 'uni.request'
      },
      header: {
          'custom-header': 'hello' //自定义请求头信息
      },
      success: (res) => {
          console.log(res.data);
      }
  });
  ```

- 上传文件

  ```javascript
  uni.chooseImage({
      count: 1,
      success: (res) => {
          uni.uploadFile({
              url: apiUtil.mainUrl + '/prod-api/common/upload',
              filePath: res.tempFilePaths[0],
              name: 'file',
              header: {
                  'Authorization': uni.getStorageSync('token')
              },
              success: (res) => {
                  let data = JSON.parse(res.data)
                  this.$put(apiUtil.modifyInfo, {
                      avatar: data.fileName
                  }).then((res) => {
                      this.$toast(res.msg)
                      if(res.code == 200){
                          this.avatar = apiUtil.mainUrl + '/prod-api' + data.fileName
                      }
                  })
              }
          })
      }
  })
  ```

## 条件编译

写法：以 #ifdef 或 #ifndef 加 %PLATFORM% 开头，以 #endif 结尾

- \#ifdef：if defined 仅在某平台存在
- \#ifndef：if not defined 除了某平台均存在
- %PLATFORM%：平台名称

| 条件编译写法                                             | 说明                                                         |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| #ifdef **APP-PLUS** 需条件编译的代码 #endif              | 仅出现在 App 平台下的代码                                    |
| #ifndef **H5** 需条件编译的代码 #endif                   | 除了 H5 平台，其它平台均存在的代码                           |
| #ifdef **H5** \|\| **MP-WEIXIN** 需条件编译的代码 #endif | 在 H5 平台或微信小程序平台存在的代码（这里只有\|\|，不可能出现&&，因为没有交集） |

**%PLATFORM%** **可取值如下：**

| 值                      | 生效条件                                                     |
| :---------------------- | :----------------------------------------------------------- |
| VUE3                    | HBuilderX 3.2.0+                                             |
| APP-PLUS                | App                                                          |
| APP-PLUS-NVUE或APP-NVUE | App nvue 页面                                                |
| APP-ANDROID             | App Android 平台 仅限 uts文件                                |
| APP-IOS                 | App iOS 平台 仅限 uts文件                                    |
| H5                      | H5                                                           |
| MP-WEIXIN               | 微信小程序                                                   |
| MP-ALIPAY               | 支付宝小程序                                                 |
| MP-BAIDU                | 百度小程序                                                   |
| MP-TOUTIAO              | 字节跳动小程序                                               |
| MP-LARK                 | 飞书小程序                                                   |
| MP-QQ                   | QQ小程序                                                     |
| MP-KUAISHOU             | 快手小程序                                                   |
| MP-JD                   | 京东小程序                                                   |
| MP-360                  | 360小程序                                                    |
| MP                      | 微信小程序/支付宝小程序/百度小程序/字节跳动小程序/飞书小程序/QQ小程序/360小程序 |
| QUICKAPP-WEBVIEW        | 快应用通用(包含联盟、华为)                                   |
| QUICKAPP-WEBVIEW-UNION  | 快应用联盟                                                   |
| QUICKAPP-WEBVIEW-HUAWEI | 快应用华为                                                   |

## 数据缓存

https://uniapp.dcloud.net.cn/api/storage/storage.html#

- uni.setStorage(OBJECT)

  将数据存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个异步接口

  ```js
  uni.setStorage({
  	key: 'storage_key', // 本地缓存中的指定的 key
  	data: 'hello', // 需要存储的内容
  	success: function () { // 接口调用成功的回调函数
  		console.log('success');
  	}
  });
  ```

- uni.setStorageSync(KEY,DATA)

  将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个同步接口

  ```js
  try {
  	uni.setStorageSync('storage_key', 'hello');
  } catch (e) {
  	// error
  }
  ```

- uni.getStorage(OBJECT)

  从本地缓存中异步获取指定 key 对应的内容

  ```js
  uni.getStorage({
  	key: 'storage_key', // 本地缓存中的指定的 key
  	success: function (res) { // 接口调用的回调函数，res = {data: key对应的内容}
  		console.log(res.data);
  	}
  });
  ```

- uni.getStorageSync(KEY)

  从本地缓存中同步获取指定 key 对应的内容

  ```js
  try {
  	const value = uni.getStorageSync('storage_key');
  	if (value) {
  		console.log(value);
  	}
  } catch (e) {
  	// error
  }
  ```

- uni.getStorageInfo(OBJECT)

  异步获取当前 storage 的相关信息

  ```js
  uni.getStorageInfo({
  	success: function (res) {
  		console.log(res.keys); // 当前 storage 中所有的 key
  		console.log(res.currentSize); // 当前占用的空间大小, 单位：kb
  		console.log(res.limitSize); // 限制的空间大小, 单位：kb
  	}
  });
  ```

- uni.getStorageInfoSync()

  同步获取当前 storage 的相关信息

  ```js
  try {
  	const res = uni.getStorageInfoSync();
  	console.log(res.keys);
  	console.log(res.currentSize);
  	console.log(res.limitSize);
  } catch (e) {
  	// error
  }
  ```

- uni.removeStorage(OBJECT)

  从本地缓存中异步移除指定 key

  ```js
  uni.removeStorage({
  	key: 'storage_key', // 本地缓存中的指定的 key
  	success: function (res) { // 接口调用的回调函数
  		console.log('success');
  	}
  });
  ```

- uni.removeStorageSync(KEY)

  从本地缓存中同步移除指定 key

  ```js
  try {
  	uni.removeStorageSync('storage_key');
  } catch (e) {
  	// error
  }
  ```

- uni.clearStorage()

  清理本地数据缓存

  ```js
  uni.clearStorage();
  ```

