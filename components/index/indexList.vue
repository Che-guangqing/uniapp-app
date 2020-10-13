<template>
	<view class="index-list animated fadeInLeft fast">
		<view class="row-1 u-f-jsb-ac">
			<view class="left u-f-ac">
				<image class="head" :src="item.userHead" mode="widthFix" lazy-load></image>
				{{item.userName}}
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
			<image class="content-img" :src="item.titlePic" mode=""></image>
			<!-- 视频及播放按钮 -->
			<view class="video-warp u-f-jsc-ac" v-if="item.type === 'video'">
				<view class="video icon iconfont icon-iconset0481"></view>
				<view class="play-info ">{{item.playNum}}W次播放 {{item.long}}</view>
			</view>
		</view>
		<view class="row-4 u-f-jsb-ac">
			<view class="u-f-ac">
				<view class="u-f-ac " :class="{'active': item.infoNum.index=== 1}" @tap="onHandle('ding')">
					<view class="icon iconfont icon-xiaolian"></view>
					<view class="b-left">{{item.infoNum.dingNum}}</view>
				</view>
				<view class="u-f-ac" :class="{'active': item.infoNum.index=== 2}" @tap="onHandle('cai')">
					<view class="icon iconfont icon-kulian"></view>
					<view class="b-left">{{item.infoNum.caiNum}}</view>
				</view>
			</view>
			<view class="u-f-ac">
				<view class="icon iconfont icon-yiliaohangyedeICON--copy"></view>
				<view class="b-left">{{item.commentNum}}</view>
				<view class="icon iconfont icon-zhuanfa"></view>
				<view class="b-left">{{item.shareNum}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
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
	/* 封装flex布局 */
	.u-f,
	.u-f-ac,
	.u-f-jsb-ac,
	.u-f-jsc-ac {
		display: flex;
	}

	.u-f-ac,
	.u-f-jsb-ac,
	.u-f-jsc-ac {
		align-items: center;
	}

	.u-f-jsb-ac {
		justify-content: space-between;
	}

	.u-f-jsc-ac {
		justify-content: center;
	}

	.index-list {
		padding: 20upx;
		border-bottom: 1upx solid #eee;
	}

	.row-1 {
		/* 	display: flex;
		justify-content: space-between;
		align-items: center; */
	}

	.left {
		/* 		display: flex;
		align-items: center; */
		color: #999999;
	}

	.head {
		width: 90upx;
		height: 90upx;
		border-radius: 50%;
		/* border: 1px solid #929292; */
		margin-right: 20upx;
	}

	.right {
		/* 		display: flex;
		align-items: center; */
	}

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
		/* right: 20upx;
		bottom: 20upx; */
	}

	.content-img {
		width: 100%;
		height: 400upx;
		border-radius: 20upx;
	}

	.row-4 {
		/* 		display: flex;
		justify-content: space-between;
		align-items: center; */
		color: #999999;
		/* font-size: 35upx; */
	}

	.bottom {
		/* 		display: flex;
		align-items: center; */
	}

	.active {
		color: #c5f68c;
	}

	.b-left {
		margin: 0 18upx
	}
</style>
