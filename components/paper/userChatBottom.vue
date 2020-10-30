<template>
	<!-- 输入框 -->
	<view class="user-chat-bottom u-f-ac">
		<input type="text" placeholder="文明发言" v-model="text"/>
		<view class="iconfont icon icon-fabu u-f-jsc-ac" @tap="submit"></view>
	</view>
</template>

<script>
	export default{
		props:{
			
		},
		data() {
			return {
				text:''
			}
		},
		methods:{
			submit() {
				// console.log(this.text) 
				this.$emit('submit', this.text)
				this.text =''
			}
		}
	}
</script>

<style scoped>
	.user-chat-bottom{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		height: 120rpx;
		padding: 0 20rpx;
		background-color: #FFFFFF;
		border-top: 1rpx solid #EEEEEE;
	}
	.user-chat-bottom>input{
		/* border: 1rpx solid red; */
		background-color: #F7F7F7;
		flex: 1;
		margin-right: 20rpx;
		padding: 10rpx 20rpx;
		border-radius: 10rpx;
	}
	.user-chat-bottom>view{
		width: 80rpx;
		/* background-color: orange; */
		font-size: 45rpx;
	}
</style>
