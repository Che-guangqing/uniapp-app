<template>
	<view>
		<!-- 背景图 + 用户信息 -->
		<user-space-head :userinfo="userinfo"></user-space-head>
		<!-- 统计 -->
		<view class="user-space-data">
			<my-data :homeData="homeData"></my-data>
		</view>
		<view class="user-space-line"></view>
		<!-- tab导航 -->
		<swiper-tab-head 
		  :tabBars="tabBars" 
		  :tabIndex="tabIndex" 
		  @tabTap='tabTap' 
		  scrollStyle="border-bottom: 0"
		  scrollItemStyle="width:33.3%">
		 </swiper-tab-head>
		 
		 <block v-for="(item,index) in tabList" :key="index">
			 <template v-if="tabIndex==0">
				 <!-- 主页 用户信息 -->
				 <user-space-userinfo :userinfo='userinfo'></user-space-userinfo>
			 </template>
		 	<template v-else-if="tabIndex==index">
		 		<!-- 列表 -->
		 		<block v-for="(list,listIndex) in item.list" :key="listIndex">
		 			<common-list :item="list" :index="listIndex"></common-list>
		 		</block>
		 		<!-- 上拉加载 -->
		 		<load-more :loadText="item.loadText"></load-more>
		 	</template>
		 </block>
		 <!-- 操作菜单 -->
		 <user-space-popup :isShow="isShow" @hide="togleShow" @delFriend="delFriend" @editName="editName"></user-space-popup>
	</view>
</template>

<script>
	import userSpaceHead from '../../components/userSpace/userSpaceHead.vue'
	import myData from '../../components/my/myData.vue'
	import swiperTabHead from '../../components/index/swiperTabHead.vue' //tabbar
	import userSpaceUserinfo from '../../components/userSpace/userSpaceUserinfo.vue' 
	import commonList from '../../components/common/commonList.vue' // 公共列表
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	import userSpacePopup from '../../components/userSpace/userSpacePopup.vue' //上拉加载更多
	export default {
		components: {
			userSpaceHead,
			myData,
			swiperTabHead,
			userSpaceUserinfo,
			commonList,
			loadMore,
			userSpacePopup
		},
		data() {
			return {
				isShow:false,
				userinfo: {
					bgImg: 1,
					userPic:"../../static/img/head.jpg",
					userName:"车车",
					sex:'女',
					age:18,
					isGuanzhu:false,
					regtime:"2019-12-11", //注册时间
					id: 12312,
					birthday:"1996-10-25",
					job:'IT',
					path:'陕西-西安',
					qg:'未婚'
				},
				homeData:[
					{ name:'获赞',num:'10k' },
					{ name:'关注',num:11 },
					{ name:'粉丝',num:12},
				],
				tabIndex: 0,
				tabBars: [{
						name: '主页',
						id: 'zhuye'
					},
					{
						name: '糗事',
						id: 'qiushi'
					},
					{
						name: '动态',
						id: 'dongtai'
					}
				],
				tabList: [ 
					    {},
					   {
						loadText: '上拉加载更多',
						list: [{
							userHead: '../../static/img/head.jpg',
							userName: '昵称',
							sex: '男',
							age: 25,
							address: '陕西 西安',
							isGuanzhu: false,
							title: '我是标题,略略略',
							titlePic: '',
							dianzan: 181,
							commentNum: 130,
							shareNum: 132,
							video: false,
							share: false
						}, {
							userHead: '../../static/img/head4.jpeg',
							userName: '昵称',
							sex: '男',
							age: 25,
							address: '陕西 西安',
							isGuanzhu: false,
							title: '我是标题,略略略',
							titlePic: '../../static/img/bg1.jpg',
							dianzan: 181,
							commentNum: 130,
							shareNum: 132,
							video: false,
							share: false
						}, {
							userHead: '../../static/img/head1.jpg',
							userName: '昵称',
							sex: '女',
							age: 25,
							address: '陕西 西安',
							isGuanzhu: false,
							title: '我是标题,略略略',
							titlePic: '../../static/img/bg.jpg',
							dianzan: 181,
							video: {
								playNum: 2000,
								long: '13:26'
							},
							share: false,
							commentNum: 130,
							shareNum: 132,
						}]
					},
					{
						loadText: '上拉加载更多',
						list: [{
							userHead: '../../static/img/head1.jpg',
							userName: '昵称',
							sex: '女',
							age: 25,
							address: '陕西 西安',
							isGuanzhu: false,
							title: '我是标题,略略略',
							titlePic: '../../static/img/bg.jpg',
							dianzan: 181,
							video: {
								playNum: 2000,
								long: '13:26'
							},
							share: false,
							commentNum: 130,
							shareNum: 132,
						}, {
							userHead: '../../static/img/head4.jpeg',
							userName: '昵称',
							sex: '男',
							age: 25,
							address: '陕西 西安',
							isGuanzhu: false,
							title: '我是标题,略略略',
							titlePic: '../../static/img/bg1.jpg',
							dianzan: 181,
							commentNum: 130,
							shareNum: 132,
							video: false,
							share: false
						}]
					}
				]
			}
		},
		// 监听原生导航栏按钮事件
		onNavigationBarButtonTap(e) {
			if(e.index === 0) {
				this.togleShow()
			}
		},
		methods: {
			// 操作显示与隐藏
			togleShow() {
				this.isShow = !this.isShow
			},
			// 拉黑
			delFriend() {
				console.log('拉黑')
				this.togleShow()
			},
			// 备注
			editName() {
				console.log('备注')
				this.togleShow()
			},
			// 监听子组件中的tabTap事件
			tabTap(index) {
				this.tabIndex = index
			},
			// 上拉加载更多
			loadMore() {
				if (this.tabList[this.tabIndex].loadText != '上拉加载更多') {
					return
				}
				// 修改数据
				this.tabList[this.tabIndex].loadText = '加载中...'
				// 获取数据
				setTimeout(() => {
					// 获取完成
					let obj = {
						userHead: '../../static/img/head4.jpeg',
						userName: '昵称',
						sex: '男',
						age: 25,
						address: '陕西 西安',
						isGuanzhu: false,
						title: '我是标题,略略略',
						titlePic: '../../static/img/bg3.jpg',
						dianzan: 181,
						commentNum: 130,
						shareNum: 132,
						video: false,
						share: false
					}
					this.tabList[this.tabIndex].list.push(obj)
					this.tabList[this.tabIndex].loadText = '上拉加载更多'
				}, 800)
				// this.tabList[this.tabIndex].loadText='没有数据啦'				
			},
			// 页面上拉触底事件处理函数
			onReachBottom() {
				this.loadMore()
			},
		}
	}
</script>

<style scoped>
	.user-space-margin {
		margin: 15rpx 0;
	}
	.user-space-data{
		background-color: #FFFFFF;
		position: relative;
		z-index: 10;
		border-top-left-radius: 20rpx;
		border-top-right-radius: 20rpx;
		margin-top: -20rpx;
	}
	.user-space-line{
		height: 20rpx;
		background-color: #F4F4F4;
	}
</style>
