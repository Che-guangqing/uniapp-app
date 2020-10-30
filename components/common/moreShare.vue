<template>
	<view class="animated fadeIn fast" v-if="show">
		<view class="more-shore-model" @tap="togle"></view>
		<view class="more-shore">
			<view class="more-share-title u-f-jsc-ac">分享到</view>
			<scroll-view scroll-x class="more-share-body u-f">
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-weixin wx"></view>
					<view class="">微信</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-xinlangweibo xlwb"></view>
					<view class="">新浪微博</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-QQ qqhy"></view>
					<view class="">QQ好友</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-weixin wx"></view>
					<view class="">微信</view>
				</view>
				<view class="more-share-item" hover-class="more-share-hover">
					<view class="icon iconfont icon-QQ qqhy"></view>
					<view class="">其他</view>
				</view>
			</scroll-view>
			<view class="more-share-bottom u-f-jsc-ac" hover-class="more-share-hover" @tap="togle">取消</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			show:Boolean
		},
		methods:{
			togle() {
				this.$emit('togle')
			}
		}
	}
</script>

<style scoped>
	/* 分享 */
	.more-shore-model {
		background-color: rgba(51, 52, 51, 0.49);

		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		z-index: 100;
	}

	.more-shore {
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		background-color: #FFFFFF;
		z-index: 110;
	}

	.more-share-title,
	.more-share-bottom {
		font-size: 32rpx;
		padding: 25rpx;
	}

	.more-share-body {
		display: flex;
		white-space: nowrap;
		width: 100%;
		height: 200rpx;
		line-height: 200rpx;
		border-bottom: 1px solid #EEEEEE;
	}

	.more-share-item {
		display: inline-flex;
		width: 25%;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100%;
	}

	.more-share-hover {
		background-color: #EEEEEE;
	}

	.wx {
		background-color: #2ad19b;
	}

	.xlwb {
		background-color: #ee5e5e;
	}

	.qqhy {
		background-color: #4a73ba;
	}

	.more-share-item>view:first-child {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		flex-shrink: 0;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 55rpx;
		color: #FFFFFF;
	}

	.more-share-item>view:last-child {
		color: #7a7a7a;
	}
</style>
