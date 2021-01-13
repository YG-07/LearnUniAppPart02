<template>
	<view id="cpn1">
		<view>这是cpn1</view>
		<button type="primary" @click="addNum">修改cpn2的数据</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		methods:{
			addNum(){
				uni.$emit('updateNum',8)
			}
		}
	}
</script>

<style>
</style>
