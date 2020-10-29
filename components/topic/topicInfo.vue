<template>
	<view>
		<!-- 模糊背景 -->
		<view class="topic-bg">
			<image :src="item.titlePic" mode="aspectFill" lazy-load></image>
		</view>
		<!-- 话题信息 -->
		<view class="topic-info">
			<view class="topic-info-top u-f-ac">
				<image :src="item.titlePic" mode="widthFix" lazy-load></image>
				<view>#{{item.title}}#</view>
			</view>
			<view class="topic-info-mid u-f-ac">
				<view class="">动态 {{item.totalNum}}</view>
				<view class="">今日 {{item.todayNum}}</view>
			</view>
			<view class="topic-info-bottom">
				{{item.desc}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			item: Object
		}
	}
</script>

<style scoped>
	.topic-bg{
		width: 100%;
		height: 300rpx;
		position: relative;
		overflow: hidden;
	}
	.topic-bg>image{
		width: 100%;
		position: absolute;
		filter: blur(10px);
	}
	.topic-info{
		padding: 0 25rpx;
	}
	.topic-info-top{
		position: relative;
	}
	.topic-info-top>image{
		width: 150rpx;
		height: 150rpx;
		border-radius: 20rpx;
		position: absolute;
		top: -75rpx;
	}
	.topic-info-top>view{
		flex: 1;
		font-size: 35rpx;
		margin-left: 170rpx;
	}
	.topic-info-mid{
		padding: 35rpx 0 10rpx 0;
		color: #cdcdcd;
	}
	.topic-info-bottom{
		color: #a3a3a3;
		font-size: 32rpx;
		padding-bottom: 10rpx;
	}
</style>
