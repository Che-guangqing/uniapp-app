<template>
	<view class="index-list u-f animated fadeInLeft fast">
		<view class="list-left">
			<image class="head" :src="item.userHead" mode="widthFix" lazy-load></image>
		</view>
		<view class="list-right">
			<view class="row-1 u-f-jsb-ac">
				<view class="left u-f-ac">
					<view class="name">{{item.userName}}</view>
					<tag-sex :sex="item.sex" :age="item.age"></tag-sex>
<!-- 					<view class="icon-warp u-f-jsc-ac" :class="{'blue-icon':item.sex==='男','red-icon':item.sex==='女'}">
						<view :class="{'sex':true,'icon iconfont icon-nan':item.sex==='男','icon iconfont icon-nv':item.sex==='女'}"></view>
						{{item.age}}
					</view> -->
				</view>
				<view class="right u-f-ac" v-show="!item.isGuanzhu">
					<view class="follow" @tap="onFollow">
						<view class="icon iconfont icon-jia"></view>
						<view>关注</view>
					</view>
					<view class="icon iconfont icon-guanbi1"></view>
				</view>
			</view>
			<view class="row-2" @click="openDetail">
				{{item.title}}
			</view>
			<view class="row-3 u-f-jsc-ac" @click="openDetail">
				<!-- 图片模式 -->
				<image v-if="item.titlePic" class="content-img" :src="item.titlePic" mode=""></image>
				<!-- 视频模式 -->
 				<view class="video-warp u-f-jsc-ac" v-if="item.video">
					<view class="video icon iconfont icon-iconset0481"></view>
					<view class="play-info ">{{item.video.playNum}}W次播放 {{item.video.long}}</view>
				</view>
				<!-- 分享模式 -->
				<view class="common-list-share u-f-ac" v-if="item.share">
					<image class="share-img" :src="item.share.sharepic" mode="widthFix" lazy-load></image>
					<view >{{item.share.title}}，</view>
				</view>
			</view>
			<view class="row-4 u-f-jsb-ac">
				<view class="address">
					{{item.address}}
				</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa"></view>
					<view class="b-left">{{item.shareNum}}</view>
					<view class="icon iconfont icon-yiliaohangyedeICON--copy"></view>
					<view class="b-left">{{item.commentNum}}</view>
					<view class="icon iconfont icon-dianzan"></view>
					<view class="b-left">{{item.dianzan}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import tagSex from './tagSex.vue'
	export default {
		components:{
			tagSex
		},
		props: {
			item: Object,
			index: Number
		},
		data() {
			return {

			}
		},
		methods: {
			// 关注
			onFollow() {
				this.item.isGuanzhu=true;
				uni.showToast({
					title:'关注成功！',
				})
			},
			// 顶 踩操作
			onHandle(type){
				// infoNum: {
				// 	index: 2, //0：没有操作，1：顶过，2：踩过
				// 	dingNum: 111,
				// 	caiNum: 180
				// },
				switch (type){
					case 'ding':
					// 已经顶过
					if(this.item.infoNum.index ==1){
						return
					}
					this.item.infoNum.dingNum ++
					// 已经踩过
					if(this.item.infoNum.index ==2){
						this.item.infoNum.caiNum --
					}
					// 标志操作了 顶
					this.item.infoNum.index=1
						break;
					case 'cai':
					// 已经踩过
					if(this.item.infoNum.index ==2){
						return
					}
					this.item.infoNum.caiNum ++
					// 已经顶过
					if(this.item.infoNum.index ==1){
						this.item.infoNum.dingNum --
					}
					// 标志操作了 顶
					this.item.infoNum.index=2
						break;
				}
			},
			// 进入详情页
			openDetail(){
				console.log('进入详情页')
			}
		}
	}
</script>

<style scoped>
	.index-list {
		/* display: flex; */
		padding: 20upx;
		border-bottom: 1upx solid #eee;
	}
	.list-left{
		width: 100rpx;
	}
	.list-right{
		flex: 1;
	}

	.left {
		color: #999999;
	}
	.name{
		margin-right: 20rpx;
	}
	.head {
		width: 90upx;
		height: 90upx;
		border-radius: 50%;
		/* border: 1px solid #929292; */
		margin-right: 20upx;
	}
/* 	.icon-warp{
		width: 72rpx;
		height: 32rpx;
		line-height: 32rpx;
		text-align: center;
		border-radius: 25rpx;
		margin-left: 20rpx;
		color: #FFFFFF;
		font-size: 12rpx;
	}
	.sex{
		font-size: 6rpx;
		margin-right: 5rpx;
	}
	.blue-icon{
		background-color: #0A98D5;	
	}
	.red-icon{
		background-color:#DD4A68;	
	} */
	.follow {
		display: flex;
		align-items: center;
		padding: 5upx 10upx;
		width: 90upx;
		height: 40upx;
		background-color: #f4f4f4;
		border-radius: 5upx;
		margin-right: 15upx;
		font-size: 20upx;
	}
	.row-2 {
		font-size: 35upx;
		padding-top: 15upx;
	}

	.row-3 {
		padding-top: 15upx;
		position: relative;
	}
/* 状态一 */
	.video-warp {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}

	.play-info {
		position: absolute;
		right: 10upx;
		bottom: 10upx;
		font-size: 25upx;
		background: rgba(51, 51, 51, 0.72);
		color: #FFFFFF;
		padding: 3upx 10upx;
		border-radius: 20upx;
	}

	.video {
		position: absolute;
		color: #FFFFFF;
		font-size: 100upx;
	}

	.content-img {
		width: 100%;
		height: 400upx;
		border-radius: 20upx;
	}
	/* 状态二 */
	.common-list-share{
		background-color: #EEEEEE;
		width: 100%;
		padding: 10upx;
		border-radius: 10upx;
	}
	.share-img{
		width: 200upx;
		height: 150upx;
		margin-right: 10rpx;
		flex-shrink: 0;
	}
	.row-4 {
		color: #999999;
	}
    .address{
		font-size: 25rpx;
	}
	.active {
		color: #c5f68c;
	}

	.b-left {
		margin: 0 18upx
	}
</style>
