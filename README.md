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
