<template>
	<view class="topic-list u-f animated fadeInLeft fast" @tap="openDetail">
		<image :src="item.titlePic" mode="widthFix" lazy-load></image>
		<view>
			<view class="list-title">#{{item.title}}#</view>
			<view class="list-des">{{item.desc}}</view>
			<view class="list-des">动态 {{item.totalNum}} 今日 {{item.todayNum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods:{
			openDetail() {
				uni.navigateTo({
					url:"../../pages/topicDetail/topicDetail"
				})
			}
		}
	}
</script>

<style>
	/* 最近更新 */
/* 	.topic-new {
		padding: 20rpx;
	}

	.topic-new>view:first-child {
		padding-bottom: 10rpx;
		font-size: 32rpx;
	} */

	.topic-list {
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEEEEE;
	}

	.topic-list image {
		width: 250rpx;
		height: 250rpx;
		border-radius: 10rpx;
		margin-right: 20rpx;
	}

	.list-title {
		color: #333333;
		font-size: 32rpx;
	}

	.list-des {
		color: #a4a4a4;
	}
</style>
