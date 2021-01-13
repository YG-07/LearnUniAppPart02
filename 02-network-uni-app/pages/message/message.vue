<template>
	<view>
		<view class="part10-upload_image">
			<view>上传图片和预览</view>
			<button type="primary" @click="upImg">上传图片</button>
			<image mode="aspectFit" v-for="(item,index) in imgArr" :src="item"
			@click="imgPre(item)"></image>
		</view>
		<view class="part11-ifdef">
			<view>这是一段文字....！</view>
			<view>条件编译</view>
			<!-- #ifdef H5 -->
			<view>我只在H5页面显示</view>
			<!-- #endif -->
			<!-- #ifdef MP-WEIXIN -->
			<view>我只在微信小程序中显示</view>
			<!-- #endif -->
		</view>
		<view class="part12-component">使用组件</view>
		<view class="part13-communication">组件通信</view>
		<view>
			<button type="warn" @click="chgCpn">销毁和加载组件</button>
			<test v-if="isMount" :communi="communi" @myEven="getData"></test>
		</view>
		
	</view>
</template>

<script>
	import test from '../../components/test.vue'
	export default{
		components:{
			test
		},
		data(){
			return{
				isMount:false,
				imgArr:[],
				communi:{
					name:'message',
					cate:'vue',
					size:1024
				},
				sonData:[]
			}
		},
		methods:{
			upImg () {
				uni.chooseImage({
					count:5,
					success: res => {
						this.imgArr = res.tempFilePaths
						console.log('上传成功',res)
						console.log(this.imgArr)
					}
				})
			},
			imgPre(current) {
				uni.previewImage({
					current,
					urls:this.imgArr,
					// 开启循环预览
					loop:true
				})
			},
			chgCpn(){
				this.isMount=!this.isMount
			},
			getData(arr){
				this.sonData = arr
				console.log('子传父成功!',this.sonData)
			}
		},
		onLoad() {
			// #ifdef H5
			console.log('我只在h5中打印')
			// #endif
			// #ifdef MP-WEIXIN
			console.log('我只在微信小程序中打印')
			// #endif
		}
	}	
</script>

<style>
	.part11-ifdef{
		/* #ifdef H5 */
		color: #FAB1A0;
		/* #endif */
		/* #ifdef MP-WEIXIN */
		color: #00B894;
		/* #endif */
	}
</style>
