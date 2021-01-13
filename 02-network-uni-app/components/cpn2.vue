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
		}
	}
</script>

<style>
	#cpn2 {
		border: #000000 1px solid;
	}
</style>
