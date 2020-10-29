<template>
	<view >
		<view class="topic-nav">
			<view class="one-row u-f-jsb-ac">
				<view class="hot-type">热门分类</view>
				<view class="u-f-ac more-large" @tap="openTopicNav">更多<view class="icon iconfont icon-jinru"></view>
				</view>
			</view>
			<view class="two-row u-f-ac">
				<block v-for="(item,index) in nav" :key="index">
					<view class="u-f-jsc-ac">{{item.name}}</view>
				</block>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		props:{
			nav: Array
		},
		methods:{
			openTopicNav() {
				uni.navigateTo({
					url:"../../pages/topicNav/topicNav"
				})
			}
		}
	}
</script>

<style scoped>
	/* 热门分类 */
	.topic-nav{
		border-top: 1rpx solid #EEEEEE;
		border-bottom: 1rpx solid #EEEEEE;
		padding: 20rpx;
	}
	.one-row{
		margin-bottom: 10rpx;
	}
	.hot-type{
		color: #333333;
		font-size: 32rpx;
	}
	.more-large{
		color: #9e9e9e;
	}
	.two-row>view{
		flex: 1;
		background-color: #EEEEEE;
		color: #9e9e9e;
		border-radius: 10rpx;
		margin: 0 10rpx;
		text-align: center;
	}
</style>
