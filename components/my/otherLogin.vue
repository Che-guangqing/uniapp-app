<template>
	<!-- 第三方登录 -->
	<view class="other-login u-f-jsc-ac">
		<view class="u-f-jsc-ac icon-warp">
			<view class="icon iconfont icon-weixin u-f-jsc-ac"></view>
		</view>
		<view class="u-f-jsc-ac icon-warp">
			<view class="icon iconfont icon-xinlangweibo u-f-jsc-ac"></view>
		</view>
		<view class="u-f-jsc-ac icon-warp">
			<view class="icon iconfont icon-QQ u-f-jsc-ac"></view>
		</view>
	</view>
</template>

<script>
</script>

<style scoped>
	.other-login {
		padding: 20rpx 80rpx;
	}
	
	.icon-warp {
		flex: 1;
	}
	
	.icon-warp>.iconfont {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		font-size: 55rpx;
		color: #FFFFFF;
	}
	
	.icon-weixin {
		background-color: #2bd19b;
	}
	
	.icon-xinlangweibo {
		background-color: #fc7729;
	}
	
	.icon-QQ {
		background-color: #2caefc;
	}
</style>
