<template>
	<view class="warp">
		<!-- tab切换 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabTap='tabTap' scrollStyle="border-bottom: 0"
		 scrollItemStyle="width:33%">
		</swiper-tab-head>
		<!-- 好友列表 -->
		<!-- 		<block v-for="(item,index) in list" :key="index">
			<user-list :item="item" :index="index"></user-list>
		</block> -->

		<!-- 每个顶部选项对应的数据 -->
		<swiper class="swiper-box" :style="{height:swiperHeight+'px'}" :current='tabIndex' @change="tabChange">
			<swiper-item class="swiper-item" v-for="(items,index) in newsList" :key='index'>
				<scroll-view class="scroll-v list" scroll-y @scrolltolower="loadMore(index)">
					<template v-if="items.list.length>0">
						<!-- 主页图文列表 -->
						<block v-for="(item,index1) in items.list" :key='index1'>
							<user-list :item="item" :index="index1"></user-list>
						</block>
						<!-- 上拉加载 -->
						<load-more :loadText="items.loadText"></load-more>
					</template>
					<template v-else>
						<!-- 无图文列表数据 显示的默认页 -->
						<no-thing></no-thing>
					</template>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	import swiperTabHead from '../../components/index/swiperTabHead.vue' //tabbar
	import userList from '../../components/paper/userList.vue' //好友列表
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	import noThing from '../../components/common/noThing.vue'
	export default {
		components: {
			swiperTabHead,
			userList,
			loadMore,
			noThing
		},
		data() {
			return {
				swiperHeight: 500, //可展示y方向滚动的区域的高度
				tabIndex: 0,
				tabBars: [{
						name: '互关',
						num: 20,
						id: 'huguan'
					},
					{
						name: '关注',
						num: 16,
						id: 'guanzhu'
					},
					{
						name: '粉丝',
						num: 40,
						id: 'fengsi'
					}
				],

				newsList: [{
						loadText: "上拉加载更多",
						list: [{
							userPic: '../../static/img/head.jpg',
							userName: '昵称',
							age: 18,
							sex: '女',
							isGuanzhu: true, // 是否关注
						}, {
							userPic: '../../static/img/head2.jpeg',
							userName: '昵称',
							age: 18,
							sex: '男',
							isGuanzhu: false, // 是否关注
						},{
							userPic: '../../static/img/head.jpg',
							userName: '昵称',
							age: 18,
							sex: '女',
							isGuanzhu: true, // 是否关注
						}, {
							userPic: '../../static/img/head2.jpeg',
							userName: '昵称',
							age: 18,
							sex: '男',
							isGuanzhu: false, // 是否关注
						},{
							userPic: '../../static/img/head.jpg',
							userName: '昵称',
							age: 18,
							sex: '女',
							isGuanzhu: true, // 是否关注
						}, {
							userPic: '../../static/img/head2.jpeg',
							userName: '昵称',
							age: 18,
							sex: '男',
							isGuanzhu: false, // 是否关注
						},{
							userPic: '../../static/img/head.jpg',
							userName: '昵称',
							age: 18,
							sex: '女',
							isGuanzhu: true, // 是否关注
						}, {
							userPic: '../../static/img/head2.jpeg',
							userName: '昵称',
							age: 18,
							sex: '男',
							isGuanzhu: false, // 是否关注
						},{
							userPic: '../../static/img/head.jpg',
							userName: '昵称',
							age: 18,
							sex: '女',
							isGuanzhu: true, // 是否关注
						}, {
							userPic: '../../static/img/head2.jpeg',
							userName: '昵称',
							age: 18,
							sex: '男',
							isGuanzhu: false, // 是否关注
						}]
					},
					{
						loadText: "上拉加载更多",
						list: [{
							userPic: '../../static/img/head.jpg',
							userName: '昵称',
							age: 18,
							sex: '女',
							isGuanzhu: true, // 是否关注
						}, {
							userPic: '../../static/img/head2.jpeg',
							userName: '昵称',
							age: 18,
							sex: '男',
							isGuanzhu: false, // 是否关注
						}]
					},
					{
						loadText: "上拉加载更多",
						list: [{
							userPic: '../../static/img/head.jpg',
							userName: '昵称',
							age: 18,
							sex: '女',
							isGuanzhu: true, // 是否关注
						}, {
							userPic: '../../static/img/head2.jpeg',
							userName: '昵称',
							age: 18,
							sex: '男',
							isGuanzhu: false, // 是否关注
						}]
					}
				]
			}
		},
		methods: {
			// 监听子组件中的tabTap事件
			tabTap(index) {
				this.tabIndex = index
			},
			// swiper滑动改变tabbar
			tabChange(e) {
				this.tabIndex = e.detail.current
				// console.log(e.detail.current)
			},
			// 触底事件
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
						userPic: '../../static/img/head2.jpeg',
						userName: '昵称',
						age: 18,
						sex: '男',
						isGuanzhu: false, // 是否关注
					}
					this.newsList[index].list.push(obj)
					this.newsList[index].loadText = '上拉加载更多'
				}, 800)
				// this.newsList[index].loadText='没有数据啦'
				// 注意： 触底事件失效：scroll-view必须设置高度
			}
		},
		// 监听导航按钮事件
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
			}
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
		}
	}
</script>

<style scoped>
	.warp {
		/* padding: 0 20rpx; */
	}
	.scroll-v {
		width: 100%;
		height: 100%;
		/* #ifndef MP-ALIPAY */
		flex-direction: column;
		/* #endif */
		width: 750rpx;
	}
</style>
