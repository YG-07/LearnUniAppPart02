<template>
	<view>
		<view>这是navigator组件</view>
		<!-- 默认左上角有返回键 -->
		<navigator url="/pages/detail/detail"><button>跳转至详情页</button></navigator>
		<!-- 重定向，返回上2层的路径 -->
		<navigator url="/pages/detail/detail" open-type="redirect"><button>卸载式跳转至详情页</button></navigator>
		<navigator url="/pages/index/index" open-type="switchTab"><button>卸载跳转至首页</button></navigator>
		<view>使用按钮点击事件</view>
		<button @click="goList">跳转至list页</button>
		<button @click="chgList">关闭并跳转至信息页</button>
		<button @click="reList">关闭并跳转至List页</button>
		<button @click="goList">传递参数到List页</button>

	</view>
</template>

<script>
	export default{
		methods:{
			goList(){
				uni.navigateTo({
					// url:"/pages/list/list"
					url:"/pages/list/list?id=90&name=Tom"
				})
			},
			chgList(){
				uni.switchTab({
					url:"/pages/message/message"
				})
			},
			reList(){
				uni.redirectTo({
					url:"/pages/list/list"
				})
			},
			toList(){
				
			}
		}
	}
</script>

<style>
</style>
