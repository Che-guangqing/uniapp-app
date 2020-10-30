<template>
	<!-- 封装消息列表组件 -->
	<view class="paper-list u-f-ac animated fadeInUpBig" @tap="openChat">
		<image :src="item.userPic" mode="widthFix" lazy-load></image>
		<view class="paper-list-right">
			<view class="u-f-jsb-ac">
				<view class="list-name">{{item.userName}}</view>
				<view class="list-time">{{item.time}}</view>
			</view>
			<view class="u-f-jsb-ac list-des">
				<view>{{item.data}}</view>
				<template v-if="item.noReadNum>0">
					<uni-badge :text="item.noReadNum" type="error"></uni-badge>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from '../../components/uni-badge/uni-badge.vue' // 官方角标
	export default {
		props: {
			item: Object,
			index: Number
		},
		components:{
			uniBadge
		},
		methods:{
			// 进入聊天页面
			openChat() {
				uni.navigateTo({
					url:"../../pages/userChat/userChat"
				})
			}
		}
	}
</script>

<style scoped>
	.paper-list {
		border-bottom: 1rpx solid #EEEEEE;
		padding: 20rpx 0;
	}

	.paper-list>image {
		width: 100rpx;
		height: 100rpx;
		margin-right: 20rpx;
		border-radius: 50%;
		flex-shrink: 0;
	}

	.paper-list-right {
		flex: 1;
	}

	.list-name {
		font-size: 35rpx;
	}

	.list-time {
		color: #cbcbcb;
	}

	.list-des {
		color: #999999;
	}
</style>
