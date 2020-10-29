<template>
	<view class="warp">
		<!-- tab切换 -->
		<swiper-tab-head 
		 :tabBars="tabBars" 
		 :tabIndex="tabIndex" 
		 @tabTap='tabTap' 
		 scrollStyle="border-bottom: 0"
		 scrollItemStyle="width:33%"
		>
		</swiper-tab-head>
		<!-- 好友列表 -->
		<block v-for="(item,index) in list" :key="index">
			<view class="user-list u-f-ac">
				<image :src="item.userPic" mode="widthFix" lazy-load></image>
				<view class="middle">
					<view class="name">{{item.userName}}</view>
					<view><tag-sex :sex="item.sex" :age="item.age"></tag-sex></view>
				</view>
				<!-- <view class="icon iconfont icon-xuanze-yixuan u-f-ac"></view> -->
				<view class="icon iconfont u-f-ac" :class="[item.isGuanzhu? 'icon-xuanze-yixuan' :'icon-Group-' ]"></view>
			</view>
		</block>

		<!-- 76 -->
	</view>
</template>

<script>
	import swiperTabHead from '../../components/index/swiperTabHead.vue' //tabbar
	import tagSex from '../../components/common/tagSex.vue' //性别组件
	export default {
		components: {
			swiperTabHead,
			tagSex
		},
		data() {
			return {
				tabIndex: 0,
				tabBars: [{
						name: '互关',
						num:20,
						id: 'huguan'
					},
					{
						name: '关注',
						num:16,
						id: 'guanzhu'
					},
					{
						name: '粉丝',
						num:40,
						id: 'fengsi'
					}
				],
				list:[
					{
						userPic:'../../static/img/head.jpg',
						userName:'昵称',
						age:18,
						sex:'女',
						isGuanzhu:true, // 是否关注
					},{
						userPic:'../../static/img/head2.jpeg',
						userName:'昵称',
						age:18,
						sex:'男',
						isGuanzhu:false, // 是否关注
					}
				]
				
			}
		},
		methods: {
			// 监听子组件中的tabTap事件
			tabTap(index) {
				this.tabIndex = index
			},
		},
		// 监听导航按钮事件
		onNavigationBarButtonTap(e) {
			if(e.index === 0) {
				uni.navigateBack({
					delta:1
				})
			}
		}
	}
</script>

<style scoped>
	.warp{
		padding: 0 20rpx;
	}
	.user-list{
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
