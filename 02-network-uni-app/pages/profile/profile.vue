<template>
	<view class="content">
		<p>这是我的主页。。。。</p>
		<view class="part14-communication2">
			<cpn1></cpn1>
			<cpn2></cpn2>
		</view>
		<view class="part15-unicom">
			<uni-calendar :insert="true" :lunar="true" :start-date="'2019-3-2'" 
				:end-date="'2019-5-20'" @change="change"></uni-calendar>
		</view>
	</view>
</template>

<script>
	import cpn1 from '../../components/cpn1.vue'
	import cpn2 from '../../components/cpn2.vue'
	import uniCalendar from '@/components/uni-calendar/uni-calendar.vue'
	
	export default {
		data(){
			return{
				
			}
		},
		methods:{
			change(e) {
				// console.log(e);
			}
		},
		components:{
			cpn1,
			cpn2,
			uniCalendar
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
</style>
