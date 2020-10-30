<template>
	<!-- 好友列表组件 -->
	<view class="user-list u-f-ac animated fadeInLeftBig">
		<image :src="item.userPic" mode="widthFix" lazy-load></image>
		<view class="middle">
			<view class="name">{{item.userName}}</view>
			<view><tag-sex :sex="item.sex" :age="item.age"></tag-sex></view>
		</view>
		<view class="icon iconfont u-f-ac" :class="[item.isGuanzhu? 'icon-xuanze-yixuan' :'icon-Group-' ]"></view>
	</view>
</template>

<script>
	import tagSex from '../../components/common/tagSex.vue' //性别组件
	export default {
		props:{
			item:Object,
			index:Number
		},
		components:{
			tagSex
		}
	}
</script>

<style scoped>
	.user-list{
		width: 95%;
		margin: 0 auto;
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEEEEE;
	}
	.user-list>image{
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		margin-right: 20rpx;
		flex-shrink: 0;
	}
	.middle{
		flex: 1;
	}
	.name{
		font-size: 32rpx;
	}
	.iconfont{
		width: 60rpx;
		font-size: 35rpx;
	}
	.icon-xuanze-yixuan{
		color: #CCCCCC;
	}
	.icon-Group-{
		color: #f8791b;
	}
</style>
