<template>
	<view class="user-chat-item">
		<view v-if="item.gstime" class="user-chat-time u-f-jsc-ac">{{item.gstime}}</view>
		<!-- 如果是我发的消息  添加user-chat-me 类名 作用相应的样式-->
		<view class="user-chat-list u-f" :class="{'user-chat-me':item.isme}">
			<!-- 好友的头像 -->
			<image v-if="!item.isme" :src="item.userPic" mode="widthFix" lazy-load></image>
			<view class="user-chat-list-body">
				<!-- 发送文字 -->
				<text v-if="item.type === 'text'">{{item.data}}</text>
				<!-- 发送图片 -->
				<image v-if="item.type === 'img'" src="../../static/img/bg.jpg" mode="widthFix" lazy-load></image>
			</view>
			<!-- 自己的头像 -->
			<image  v-if="item.isme" :src="item.userPic" mode="widthFix" lazy-load></image>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			item:Object,
			index:Number
		},
		data() {
			return {
			}
		},
		methods:{
		}
	}
</script>

<style scoped>
	.user-chat-time{
		padding: 40rpx 0;
		color: #a2a2a2;
	}
	.user-chat-list {
		padding: 20rpx;
	}
	
	.user-chat-list>image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		flex-shrink: 0;
	}
	/* 聊天气泡 */
	.user-chat-list-body {
		position: relative;
		background-color: #F4F4F4;
		padding: 25rpx;
		margin-left: 20rpx;
		border-radius: 25rpx;
		margin-right: 100rpx;
	}
	.user-chat-list-body:after{
		position: absolute;
		left: -30rpx;
		top: 30rpx;
		right: 0;
		content: '';
		width: 0;
		height: 0;
		border: 16rpx solid #F4F4F4;
		border-color: transparent #F4F4F4 transparent transparent
	}
	.user-chat-list-body>image {
		max-width: 150rpx;
		max-height: 200rpx;
		border-radius: 10rpx;
	}
	/* 聊天 自己的样式 */
	.user-chat-me{
		justify-content: flex-end;
	}
	.user-chat-me .user-chat-list-body{
		margin-right: 20rpx;
		margin-left: 100rpx;
	}
	.user-chat-me .user-chat-list-body::after{
		left: auto;
		right: -30rpx;
		border-color: transparent transparent transparent #F4F4F4
	}
</style>
