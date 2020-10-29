<template>
	<view>
		<!-- 自定义导航栏 -->
		<view class="nav-bar u-f-jsb-ac" >
			<view class="icon iconfont icon-qiandaoicon"></view>
			<view class="u-f">
			  <view class="tab-warp u-f-jsb-ac" v-for="(item,index) in tabItem" :key='index'>
				  <view class="item" :class="{'item-active':index===tabIndex}" @tap="changeTab(index)">
					  {{item.name}}
					  <view :class="{'active':index===tabIndex}"  > </view>
				  </view>
			  </view>
			</view>
			<view class="icon iconfont icon-bi" @tap="openAdd"></view>
		</view>
		<!-- 占位 -->
		<view style="width: 100%;height: 80rpx;"></view>
		<!-- 内容 -->
		<view class="action-content">
			<swiper class="swiper-box" :style="{height:swiperHeight+'px'}" :current='tabIndex' @change="tabChange">
				<!-- 关注 -->
				<swiper-item class="swiper-item">
					<scroll-view class="scroll-v list" scroll-y @scrolltolower="loadMore()">
						<!-- 主页图文列表 -->
						<block v-for="(item,index1) in guanzhu.list" :key='index1'>
							<common-list :item='item' :index='index'></common-list>
						</block>
						<!-- 上拉加载 -->
						<load-more :loadText="guanzhu.loadText"></load-more>
					</scroll-view>
				</swiper-item>
				<!-- 话题 -->
				<swiper-item class="swiper-item">
					<scroll-view class="scroll-v list" scroll-y >
						<!-- 搜索框 -->
						<view class="search-input">
							<input class="uni-input" placeholder-class="uni-page-head-search-placeholder topic-search" placeholder="搜索内容"/>
						</view>
						<!-- 轮播图 -->
						<swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
							<block v-for="(item,index) in topic.swiper" :key="index">
								<swiper-item>
									<image  :src="item.src" mode=""></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<top-nav :nav="topic.nav"></top-nav>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view >最近更新</view>
							<block v-for="(item,index) in topic.list" :key="index">
								<topic-list :item="item" :index="index"></topic-list>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import commonList from '../../components/common/commonList.vue'
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	import topNav from '../../components/action/topicNav.vue'
	import topicList from '../../components/action/topicList.vue'
	export default {
		components:{
			commonList,
			loadMore,
			topNav,
			topicList
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					// 得到可展示的高度
					let height = res.windowHeight - uni.upx2px(100)
					this.swiperHeight = height
					// console.log(res.screenHeight); //屏幕高度
					// console.log(res.windowHeight); //窗口高度
					// console.log(height)
				}
			});
		},
		data() {
			return {
				swiperHeight: 500, //可展示y方向滚动的区域的高度
				tabItem: [
					{name:'关注',id:'guanzhu'},
					{name:'话题',id:'huati'}
				],
				tabIndex:0,
				guanzhu: {
					loadText: '上拉加载更多',
					list:[{ //分享
						userHead: '../../static/img/head1.jpg',
						userName: '昵称',
						sex:'女',
						age:25,
						address:'陕西 西安',
						isGuanzhu: false,
						title: '我是标题,略略略',
						// type: 'img', //img:图片类型， video:视频类型
						video:false,
						share:{
						    title:"我是分享的标题",
							sharepic: "../../static/img/share1.gif"
						},
						titlePic: '',
						dianzan: 181,
						commentNum: 130,
						shareNum: 132,
					},{
						userHead: '../../static/img/head4.jpeg',
						userName: '昵称',
						sex:'男',
						age:25,
						address:'陕西 西安',
						isGuanzhu: false,
						title: '我是标题,略略略',
						titlePic: '../../static/img/bg1.jpg',
						dianzan: 181,
						commentNum: 130,
						shareNum: 132,
						video:false,
						share:false
					},{
						userHead: '../../static/img/head1.jpg',
						userName: '昵称',
						sex:'女',
						age:25,
						address:'陕西 西安',
						isGuanzhu: false,
						title: '我是标题,略略略',
						titlePic: '../../static/img/bg.jpg',
						dianzan: 181,
						video:{
							playNum:2000,
							long:'13:26'
						},
						share:false,
						commentNum: 130,
						shareNum: 132,
					}]
				},
				topic: {
					swiper: [
						{src: '../../static/img/bg4.jpg'},
						{src: '../../static/img/bg3.jpg'},
						{src: '../../static/img/bg1.jpg'}
					],
					nav: [
						{name:'最新'},
						{name:'游戏'},
						{name:'打卡'},
						{name:'情感'},
						{name:'故事'},
						{name:'喜爱'},
					],
					list: [
						{
							titlePic:"../../static/img/share.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						},
						{
							titlePic:"../../static/img/share1.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						},
						{
							titlePic:"../../static/img/share.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						},{
							titlePic:"../../static/img/share.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						},
						{
							titlePic:"../../static/img/share1.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						}
					]
				}
				
			}
		},
		methods: {
			openAdd() {
				uni.navigateTo({
					url:'../addInput/addInput'
				})
			},
			changeTab(index){
				this.tabIndex = index
				console.log(index)
			},
			// 触底事件
			loadMore(index) {
				if (this.guanzhu.loadText != '上拉加载更多') {
					return
				}
				// 修改数据
				this.guanzhu.loadText = '加载中...'
				// 获取数据
				setTimeout(() => {
					// 获取完成
					let obj = {
						userHead: '../../static/img/head4.jpeg',
						userName: '昵称',
						sex:'男',
						age:25,
						address:'陕西 西安',
						isGuanzhu: false,
						title: '我是标题,略略略',
						titlePic: '../../static/img/bg1.jpg',
						dianzan: 181,
						commentNum: 130,
						shareNum: 132,
						video:false,
						share:false
					}
					this.guanzhu.list.push(obj)
					this.guanzhu.loadText = '上拉加载更多'
				}, 800)
				// this.guanzhu.loadText='没有数据啦'
				// 注意： 触底事件失效：scroll-view必须设置高度
			},
			// swiper滑动改变tabbar
			tabChange(e) {
				this.tabIndex = e.detail.current
				// console.log(e.detail.current)
			}
		}
	}
</script>

<style scoped>
	.icon-qiandaoicon{
		color: #ff9619;
		font-size: 45upx;
		margin-left: 20rpx;
	}
	.icon-bi{
		margin-right: 20rpx;
	}
	.nav-bar{
		height: 80rpx;
		border-bottom: 5rpx solid #EEEEEE ;
		width: 100%;
		margin: 0 auto;		
		position: fixed;
		z-index: 1;
		background-color: #FFFFFF;
	}
	.uni-textarea{
		border: 1upx solid #EEEEEE 
	}
	.tab-warp{
		width: 70rpx;
	}
	.item{
		color: #929292;
	}
	.item-active{
		color: #000000;
	}
	.active{
		width: 55rpx;
		height: 8rpx;
		border-radius: 10rpx;
		background-color: #fede33;
		margin-top: -5rpx;
	}
	/* swiper */
	.swiper-box {
		/* height: 700upx; */
	}

	.swiper-item {
		width: 100%;
		flex-direction: row;
		overflow: auto;
	}

	.scroll-v {
		width: 100%;
		height: 100%;
		/* #ifndef MP-ALIPAY */
		flex-direction: column;
		/* #endif */
		width: 750rpx;
	}
	/* 搜索框 */
	.search-input{
		padding: 20rpx;
		margin-top: 2px;
	}
	.uni-input{
		background-color: #F4F4F4;
		border-radius: 15rpx;
	}
	.topic-search{
		display: flex;
		justify-content: center;
		font-size: 28rpx;
	}
	/* 轮播图 */
	.topic-swiper{
		padding: 0 20rpx 20rpx 20rpx;
	}
	.topic-swiper image{
		width: 100%;
		border-radius: 10rpx;
	}
	/* 最近更新 */
	.topic-new {
		padding: 20rpx;
	}
	
	.topic-new>view:first-child {
		padding-bottom: 10rpx;
		font-size: 32rpx;
	}
</style>
