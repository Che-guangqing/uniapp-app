<template>
	<!-- 已登录信息 -->
	<view class="home-info u-f-ac" @tap='toUserSpace'>
		<image class="my-head" :src="homeInfo.userPic" mode="widthFix" lazy-load></image>
		<view class="u-f1 info-middle">
			<view>{{homeInfo.userName}}</view>
			<view>总访客 {{homeInfo.totalNum}} 今日 {{homeInfo.todayNum}}</view>
		</view>
		<view class="icon iconfont icon-jinru info-icon"></view>
	</view>
</template>

<script>
	export default{
		props:{
			homeInfo:Object
		},
		methods:{
			toUserSpace() {
				uni.navigateTo({
					url:'../../pages/userSpace/userSpace'
				})
			}
		}
	}
</script>

<style scoped>
	/*  */
	.home-info{
		padding: 20rpx 40rpx;
	}
	.my-head{
		flex-shrink: 0;
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		margin-right: 15rpx;
	}
	.info-middle{
		color: #BBBBBB;
	}
	.info-middle>view:first-of-type{
		font-size: 32rpx;
		color: #000000;
	}
	.info-icon{
		height: 100%;
	}
</style>
