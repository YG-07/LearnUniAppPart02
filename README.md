# LearnUniAppPart02
学习uni-app网络相关知识   Learn UniApp Part02

# 一、资料来源
（B站Up主**玩儿派**转载自 杭州校区黑马程序员**刘老师**）  
(20-p)B站视频：https://www.bilibili.com/video/BV1CC4y1476y?p=20

# 二、知识总结大纲
(数字表示视频分P)  
## 一、发送get请求 (20)
* 官方文档URL：https://uniapp.dcloud.io/api/request/request  
### 1.1 首先配置一个本地服务器和数据库，步骤
(配置的难点，详见视频)  
* 老师的qq空间里的**uniapp资料**及一个**项目服务器**：百度网盘：https://pan.baidu.com/share/init?surl=-jwqo5_d47iotzdlQB_FYQ 提取码：682a 
* 安装过MySQL的话，**先删除自带的mysql服务**(只会删除服务，不会删除数据库文件)，使用指令删除:`sc delete mysql`
* 下载安装phpstudy(安装目录不能有中文)，官方网站URL：https://www.xp.cn/download.html
* 然后打开软件，**先设置MySQL的数据模式：NO_ENGINE_SUBSTITUTION**(可能需要重新打开软件)
* 然后`启动WNMP`，即启动了`MySQL`和`Nginx`
* 打开数据库front软件，创建数据库，名字固定为**dtcmsdb4**，然后输入SQL文件，**编码UTF-8**：老师素材的**dtcmsdb4.sql**文件
* 在素材的heima_shop_server目录下打开cmd，安装node包，指令：`npm i` 或 `cnpm i`，然后启动服务，指令：`node ./src/app.js`
* 启动的端口默认是`8082`，打开浏览器输入URL：`http://localhost:8082/api/getlunbo`，测试接口是否成功

### 1.2 通过request发送get请求
* 定义一个点击事件调用request方法发送请求,这里获取的是老师项目的`api/getlunbo`轮播图接口
```javaScript
uni.request({
	url:"http://localhost:8082/api/getlunbo",
	success(res) {
		console.log(res)
	}
})
```
## 二、数据缓存 (21)
* 官方文档URL：https://uniapp.dcloud.io/api/storage/storage?id=setstorage
### 2.1 异步的数据缓存setStorage
* uni.setStorage(OBJECT) 将数据存储在`本地缓存`中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个**异步接口**。参数如下：
  key：本地缓存中的指定的key变量名
  data：缓存的数据
  success：存储成功回调函数
* uni.getStroage(OBJECT) 获取缓存数据，uni.removeStorage(OBJECT)移除缓存，除了没有data属性，差不多同理
```javaScript
setStor(){
	uni.setStorage({
		key:"id",
		data:80,
		success() {
			console.log("缓存成功")
		}
	})
},
getStor(){
	uni.getStorage({
		key:"id",
		success(res){
			console.log("获取成功","对象数据:",res,"数据id:",res.data)
		}
	})
},
removeId(){
	uni.removeStorage({
		key:"id",
		success() {
			console.log("删除成功")
		}
	})
}
```
### 2.2 同步的数据缓存setStorageSync
* 同步的setStorageSync的参数更加简洁，只有key和data，获取和删除差不多
```javaScript
setStor(){
	uni.setStorageSync("sync",100)
    console.log("缓存成功")
},
getStor(){
	const res=uni.getStorageSync('sync')
	// 直接就是获取data
	console.log("获取成功","对象:",res,"数据类型:",typeof res)
},
removeId(){
	uni.removeStorageSync('sync')
	console.log("移除成功")
}
```
### 2.3 查看storage缓存状态
* uni.getStorageInfo(OBJECT) 异步获取，有3个回调函数success、fail、complete(成功失败都会执行)
  * success的返回值属性有：keys、currentSize(占用的空间大小, 单位：kb)、limitSize(限制的空间大小, 单位：kb)
* uni.getStorageInfoSync() 同步获取当前 storage 的相关信息。成功的返回值同上
* uni.clearStorage()和uni.clearStorageSync() 清理本地数据缓存。后者可以使用try-catch

## 三、图片的上传和预览 (22)
* 官方文档URL：https://uniapp.dcloud.io/api/media/image
### 3.1 上传图片
* uni.chooseImage(OBJECT) 从本地相册选择图片或使用相机拍照。App端如需要更丰富的相机拍照API。OBJECT参数常用有：
	* count 最多可以选择的图片张数，默认9
	* success、fail、complete 3种回调函数
	*  sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
### 3.2 图片预览
* uni.previewImage(OBJECT) 预览图片。
	* current 为当前显示图片的链接/索引值，不填或填写的值无效则为 urls 的第一张
	* urls (必填)需要预览的图片链接列表
	* loop 循环预览，默认false（仅支持5+App）
## 四、条件编译来跨端兼容 (23)
官方文档URL：https://uniapp.dcloud.io/platform?id=%e8%b7%a8%e7%ab%af%e5%85%bc%e5%ae%b9
### 4.1 条件编译
* 支持的文件`.vue/.js/.css/pages.json和平台特有的组件`，和各预编译语言文件，如：`.scss、.less、.stylus、.ts、.pug`
* 写法：以 `#ifdef` 或 `#ifndef`(除了某平台) 加 `%PLATFORM%`(平台名称，多个就使用`||`，没有平台交集) 开头，以 `#endif` 结尾。
* %PLATFORM% 可取值(部分常用如下：
```
值	平台
APP-PLUS	App
H5	H5
MP-WEIXIN	微信小程序
MP-ALIPAY	支付宝小程序
MP	微信小程序/支付宝小程序/百度小程序/字节跳动小程序/QQ小程序/360小程序
```
## 五、导航跳转和传参 (24)
* 官方文档URL：https://uniapp.dcloud.io/api/router?id=navigateto
### 5.1 navigator标签页面跳转
* navigator该组件(标签)类似HTML中的<a>组件，但只能跳转本地页面。目标页面必须在pages.json中注册。属性有：
	* url：	应用内的跳转链接，值为**相对路径或绝对路径**，如："**../**first/first"，"**/**pages/first/first"，注意不能加 .vue 后缀
	* open-type 跳转方式，如：`switchTab跳转到tabbar导航页`，`redirect卸载此页并跳转`
### 5.2 uni.navigateTo方法跳转
* uni.navigateTo 跳转至某个页面
* uni.switchTab 跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面。
* uni.redirectTo 关闭当前页面，跳转到应用内的某个页面。
### 5.3 参数传递和接收
* 在url参数后面使用：`?属性=值&...`的方式传参，都是字符串类型
