<template>
	<view>
		<view>网络请求</view>
		<view class="part09-get">
			<view>运行代码时，注释相应的事件方法代码</view>
			<button @click="get">发送get请求</button>
			<view>
				<view>异步接口的数据缓存</view>
				<button @click="setStor" type="primary">数据缓存</button>
				<button @click="getStor">获取缓存</button>
				<button @click="removeId" type="warn" >移除缓存"id"</button>
			</view>
			<view>
				<view>同步接口的数据缓存</view>
				<button @click="setStor" type="primary">数据缓存 同步</button>
				<button @click="getStor">获取缓存 同步</button>
				<button @click="removeId" type="warn" >移除缓存"id" 同步</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		methods:{
			get(){
				uni.request({
					url:"http://localhost:8082/api/getlunbo",
					success(res) {
						console.log(res)
					}
				})
			},
			setStor(){
				// uni.setStorage({
				// 	key:"id",
				// 	data:80,
				// 	success() {
				// 		console.log("缓存成功")
				// 	}
				// })
				uni.setStorageSync("sync",100)
			},
			getStor(){
				// uni.getStorage({
				// 	key:"id",
				// 	success(res){
				// 		console.log("获取成功","对象数据:",res,"数据id:",res.data)
				// 	}
				// })
				const res=uni.getStorageSync('sync')
				// 直接就是获取data
				console.log("获取成功","对象:",res,"数据类型:",typeof res)
			},
			removeId(){
				// uni.removeStorage({
				// 	key:"id",
				// 	success() {
				// 		console.log("删除成功")
				// 	}
				// })
				uni.removeStorageSync('sync')
				console.log("移除成功")
			}
		}
	}
</script>

<style>
</style>
