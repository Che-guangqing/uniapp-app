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
			<!-- 主页图文列表 -->
			<block v-for="(item,index1) in list" :key='index1'>
				<common-list :item='item' :index='index'></common-list>
			</block>
			<!-- 上拉加载 -->
			<!-- <load-more :loadText="item.loadText"></load-more> -->
		</view>
	</view>
</template>

<script>
	import commonList from '../../components/common/commonList.vue'
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	export default {
		components:{
			commonList,
			loadMore
		},
		data() {
			return {
				tabItem: [
					{name:'关注',id:'guanzhu'},
					{name:'话题',id:'huati'}
				],
				tabIndex:0,
				list:[{ 
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
				},{ //分享
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
				}]
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
			loadMore(index) {
				if (this.newsList[index].loadText != '上拉加载更多') {
					return
				}
				// 修改数据
				this.newsList[index].loadText = '加载中...'
				// 获取数据
				setTimeout(() => {
					// 获取完成
					let obj = {
						userHead: '../../static/img/head.jpg',
						userName: '昵称',
						isGuanzhu: true,
						title: '我是标题',
						type: 'video', //img:图片类型， videoL:视频类型
						titlePic: '../../static/img/bg.jpg',
						playNum: 2000,
						long: '2:47',
						infoNum: {
							index: 2, //0：没有操作，1：顶过，2：踩过
							dingNum: 111,
							caiNum: 180
						},
						commentNum: 100,
						shareNum: 132
					}
					this.newsList[index].list.push(obj)
					this.newsList[index].loadText = '上拉加载更多'
				}, 800)
				// this.newsList[index].loadText='没有数据啦'
				// 注意： 触底事件失效：scroll-view必须设置高度
			}
			
		}
	}
</script>

<style>
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
</style>
