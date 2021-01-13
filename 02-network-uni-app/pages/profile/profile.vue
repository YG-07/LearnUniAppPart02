<template>
	<view>
		<p>这是我的主页。。。。</p>
		<view class="part14-communication2">
			<cpn1></cpn1>
			<cpn2></cpn2>
		</view>
	</view>
</template>

<script>
	import cpn1 from '../../components/cpn1.vue'
	import cpn2 from '../../components/cpn2.vue'
	
	export default {
		data(){
			return{
				
			}
		},
		components:{
			cpn1,
			cpn2
		}
	}
</script>

<style>
</style>
