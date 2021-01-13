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
	</view>
</template>

<script>
	export default{
		data(){
			return{
				imgArr:[]
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
