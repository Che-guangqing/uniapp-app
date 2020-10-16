<template>
	<view>
		<!-- 顶部选项卡 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabTap='tabTap'></swiper-tab-head>
		<!-- 每个顶部选项对应的数据 -->
		<swiper class="swiper-box" :style="{height:swiperHeight+'px'}" :current='tabIndex' @change="tabChange">
			<swiper-item class="swiper-item" v-for="(items,index) in newsList" :key='index'>
				<scroll-view class="scroll-v list" scroll-y @scrolltolower="loadMore(index)">
					<template v-if="items.list.length>0">
						<!-- 主页图文列表 -->
						<block v-for="(item,index1) in items.list" :key='index1'>
							<index-list :item='item' :index='index'></index-list>
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
	import indexList from '../../components/index/indexList.vue' //图文列表
	import swiperTabHead from '../../components/index/swiperTabHead.vue' //tabbar
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	import noThing from '../../components/common/noThing.vue' //上拉加载更多
	export default {
		components: {
			indexList,
			swiperTabHead,
			loadMore,
			noThing
		},
		data() {
			return {
				tabIndex: 0, //顶部选项切换变量
				swiperHeight: 500, //可展示y方向滚动的区域的高度
				// tabbar数据
				tabBars: [{
					name: '关注',
					id: 'guanzhu'
				}, {
					name: '推荐',
					id: 'tuijian'
				}, {
					name: '体育',
					id: 'tiyu'
				}, {
					name: '热点',
					id: 'redian'
				}, {
					name: '财经',
					id: 'caijing'
				}, {
					name: '娱乐',
					id: 'yule'
				}, {
					name: '军事',
					id: 'junshi'
				}],
				// 展示的图文类表数据
				newsList: [{
						loadText: '上拉加载更多',
						list: [{
								userHead: '../../static/img/head.jpg',
								userName: '昵称',
								isGuanzhu: false,
								title: '我是标题，我在关注项',
								type: 'img', //img:图片类型， videoL:视频类型
								titlePic: '../../static/img/bg4.jpg',
								infoNum: {
									index: 1, //0：没有操作，1：顶过，2：踩过
									dingNum: 181,
									caiNum: 10
								},
								commentNum: 130,
								shareNum: 132
							},
							{
								userHead: '../../static/img/head2.jpeg',
								userName: '昵称',
								isGuanzhu: true,
								title: '我是标题',
								type: 'video', //img:图片类型， videoL:视频类型
								titlePic: '../../static/img/bg3.jpg',
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
						],
					},
					{
						loadText: '上拉加载更多',
						list: [

							{
								userHead: '../../static/img/head3.jpg',
								userName: '昵称',
								isGuanzhu: false,
								title: '我是标题，我在推荐项',
								type: 'img', //img:图片类型， videoL:视频类型
								titlePic: '../../static/img/bg3.jpg',
								infoNum: {
									index: 0, //0：没有操作，1：顶过，2：踩过
									dingNum: 181,
									caiNum: 10
								},
								commentNum: 130,
								shareNum: 132
							},
							{
								userHead: '../../static/img/head4.jpeg',
								userName: '昵称',
								isGuanzhu: true,
								title: '我是标题',
								type: 'video', //img:图片类型， videoL:视频类型
								titlePic: '../../static/img/bg1.jpg',
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
						],
					},
					{
						loadText: '上拉加载更多',
						list: [{
								userHead: '../../static/img/head.jpg',
								userName: '昵称',
								isGuanzhu: false,
								title: '我是标题，我在体育项',
								type: 'img', //img:图片类型， videoL:视频类型
								titlePic: '../../static/img/bg4.jpg',
								infoNum: {
									index: 1, //0：没有操作，1：顶过，2：踩过
									dingNum: 181,
									caiNum: 10
								},
								commentNum: 130,
								shareNum: 132
							},
							{
								userHead: '../../static/img/head.jpg',
								userName: '昵称',
								isGuanzhu: true,
								title: '我是标题',
								type: 'video', //img:图片类型， videoL:视频类型
								titlePic: '../../static/img/bg1.jpg',
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
						],
					},
					{
						loadText: '上拉加载更多',
						list: [

						]
					},
					{
						loadText: '上拉加载更多',
						list: []
					},
					{
						loadText: '上拉加载更多',
						list: [

						]
					},
					{
						loadText: '上拉加载更多',
						list: [

						]
					},
				],
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
						userHead: '../../static/img/head1.jpg',
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
		// 监听搜索框点击事件
		onNavigationBarSearchInputClicked() {
			// console.log('打开搜索页')
			uni.navigateTo({
				url: '../search/search'
			})
		},
		// 监听原生标题栏按钮点击事件，参数为Object
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 1:
					// 发布按钮的index为1
					uni.navigateTo({
						url: '../addInput/addInput'
					})
					break;
				case value:
					break;
			}
			console.log(JSON.stringify(e.index))
		},
	}
</script>

<style>
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
</style>
