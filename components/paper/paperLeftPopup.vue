<template>
	<view>
		<view class="paper-left-popup-mask" v-show="isShow" @tap="hidePopup"></view>
		<view class="paper-left-popup" v-show="isShow">
			<view class="u-f-ac" hover-class="popup-hover" @tap="addFriend">
				<view class="icon iconfont icon-jia"></view>
				<view class="">加好友</view>
			</view>
			<view class="u-f-ac" hover-class="popup-hover" @tap="clear">
				<view class="icon iconfont icon-clean"></view>
				<view class="">清除缓存</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			isShow:Boolean
		},
		methods:{
			// 操作菜单
			// 加好友
			addFriend() {
				console.log('加好友')
				this.$emit('addFriend')
			},
			clear() {
				console.log('清除')
				this.$emit('clear')
			},
			hidePopup() {
				this.$emit('hide')
			},
			showPopup() {
				this.$emit('show')
			},
		}
	}
</script>

<style scoped>
	/* 操作菜单 */
	.paper-left-popup-mask {
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		z-index: 9998;
	}
	
	.paper-left-popup {
		position: fixed;
		right: 0;
		top: 100rpx;
		background-color: #FFFFFF;
		z-index: 9999;
		width: 350rpx;
		box-shadow: 1rpx 1rpx 20rpx 2rpx #CCCCCC;
		font-size: 35rpx;
	}
	
	.iconfont {
		padding: 15rpx;
		margin-right: 10rpx;
		font-weight: bold;
	}
	
	.popup-hover {
		background-color: #EEEEEE;
	}
</style>
