<template>
	<view class="user-space-userInfo">
		<view class="userInfo-item">
			<view >账号信息</view>
					<view >糗龄：{{getRegAge}}</view>
					<view >用户ID: {{userinfo.id}}</view>
		</view>
		<view class="userInfo-item">
			<view >个人信息</view>
					<view >星座：{{getXingzuo}}</view>
					<view >职业: {{userinfo.job}}</view>
					<view >故乡: {{userinfo.path}}</view>
					<view >情感状态: {{userinfo.qg}}</view>
		</view>
	</view>
</template>

<script>
	import t from '../../common/time.js'
	export default {
		props:{
			userinfo:Object
		},
		computed:{
			// 计算使用时间
			getRegAge() {
				return t.gettime.sumAge(this.userinfo.regtime)
			},
			// 计算星座
			getXingzuo() {
				return t.gettime.getHoroscope(this.userinfo.birthday)
			}
		},
	}
</script>

<style scoped>
	.user-space-userInfo{
		padding: 0 30rpx;
		
	}
	.userInfo-item{
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEEEEE;
		color: #AAAAAA;
	}
	.userInfo-item>view:first-child{
		color: #333333;
		font-size: 35rpx;
		padding: 15rpx 0;
	}
</style>
