<template>
	<view>
		<view>这是test组件，这是父组件的数据：</view>
		<view>父传子成功!:{{communi.name}},{{communi.cate}},{{communi.size}}</view>
		<text id='num'>数字：{{num}}</text>
		<button type="primary" @click="sendData">通信:子传父组件,发送</button>
		<view id="colorBox"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				num:3,
				intId:null,
				stuArr:['张三','李四','王五'],
				obj:{}
			};
		},
		props:[
			'communi'
		],
		methods:{
			sendData(){
				this.$emit('myEven',this.stuArr)
			}
		},
		// 实例初始化之后被调用,还没创建
		// beforeCreate() {
		// 	console.log('beforeCreate创建前，组件数据未定义,num：',this.num)
		// },
		// 实例创建完成后
		// created() {
			// this.intId = setInterval(()=>{
			// 	console.log('执行定时器')
			// },2000)
			// console.log('created创建后，组件数据num：',this.num)
		// },
	// 以下6个方法仅在H5中展示
	// 挂载开始之前被调用
		// beforeMount() {
		// 	console.log('beforeMount挂载前,num的DOM元素null：',document.getElementById('num'))
		// },
	// 挂载到实例上去之后调用(执行1次)
		// mounted() {
		// 	console.log('mounted挂载后,num的DOM元素：',document.getElementById('num'))
		// },
		// beforeUpdate() {}, //数据更新时调用 
		// updated() {}, //由于数据更改导致的虚拟 DOM 重新渲染之后 
	// 实例销毁之前调用，此时实例仍然完全可用
		// beforeDestroy() {
		// 	console.log('beforeDestroy销毁之前,num:',this.num)
		// },
	// Vue 实例销毁时调用
		// destroyed() {
		// 	clearInterval(this.intId)
		// 	console.log('销毁定时器')
		// 	console.log('destroy销毁后,num:',this.num)
		// }
	}
</script>

<style>
	/* 一个四色菱形 */
	#colorBox {
		margin: 80rpx auto;
		width: 0rpx;
		height: 0rpx;
		text-align: center;
		border-style: solid;
		border-width: 200rpx;
		border-left-color: #F67B66;
		border-top-color: #47ACF8;
		border-right-color: #85E838;
		border-bottom-color: #EFD83C;
		transform: rotate(45deg);
	}
</style>
