<template>
	<view class="user-space-head u-f-jsc-ac">
		<image class="user-bg" :src="gteBgImg" mode="widthFix" lazy-load @tap.stop='changeBgImg'></image>
		<view class="user-space-info u-f-jsc-ac u-f-column">
			<image  class="user-head" :src="userinfo.userPic" mode="widthFix" lazy-load></image>
			<view class="user-space-margin u-f-jsc-ac">
				<view class="user-name">{{userinfo.userName}}</view>
				<tag-sex :sex="userinfo.sex" :age="userinfo.age"></tag-sex>
			</view>
			<view class="icon iconfont  user-space-btn user-space-margin " :class="[isGuanzhu?'active' :'icon-jia']" @tap.stop="guanzhu">
				{{isGuanzhu?'已关注':'关注'}}
			</view>
		</view>
	</view>
</template>

<script>
	import tagSex from '../common/tagSex.vue'
	export default {
		components: {
			tagSex
		},
		props:{
			userinfo: Object
		},
		data() {
			return {
				isGuanzhu:this.userinfo.isGuanzhu
			}
		},
		methods:{
			// 关注
			guanzhu() {
				this.isGuanzhu = !this.isGuanzhu
			},
			// 切换背景
			changeBgImg() {
				let no = parseInt(this.userinfo.bgImg)
				no = no < 4 ? ++no : 1
				this.userinfo.bgImg = no
			}
		},
		computed:{
			gteBgImg() {
				return "../../static/img/userHead/bg"+this.userinfo.bgImg+".jpg"
			}
		},
	}
</script>

<style scoped>

	.user-space-head {
		position: relative;
		height: 450rpx;
		overflow: hidden;
	}
	.user-bg{
		width: 100%;
	}

	.user-space-info {
		position: absolute;
		top: 55px;
	}
	.user-head{
		width: 150rpx;
		height: 150rpx;
		border-radius: 50%;
	}
    .user-name{
		color: #FFFDEF;
		font-size: 35rpx;
		font-weight: bold;
		text-shadow: 2rpx 2rpx 10rpx #333333;
		margin-right: 10rpx;
	}
	.user-space-btn{
		background-color: #ffe933;
		border-radius: 10rpx;
		color: #333333;
		border: 1rpx solid #ffe933;
		padding: 0 15rpx;
		font-size: 28rpx;
	}
	.active{
		background-color: none;
		color:#FFFFFF ;
		border: 1rpx solid #FFFFFF;
	}
</style>
