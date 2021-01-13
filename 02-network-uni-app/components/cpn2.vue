<template>
	<view id="cpn2">
		<view>这是cpn2</view>
		<view>cpn2的数据:{{num}}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				num:10
			};
		},
		created() {
			uni.$on('updateNum',(cnt)=>{
				this.num+=cnt
			})
		}
	}
</script>

<style>

</style>
