<template>
	<view>
		<!-- 顶部选项卡 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabTap='tabTap'></swiper-tab-head>
		<swiper class="swiper-box" :style="{height:swiperHeight+'px'}" :current='tabIndex' @change="tabChange">
			<swiper-item class="swiper-item" v-for="(items,index) in newsList" :key='index'>
				<scroll-view class="scroll-v list" scroll-y @scrolltolower="loadMore(index)">
					<template v-if="items.list.length>0">
						<!-- 话题列表 -->
						<view class="topic-view">
							<block v-for="(item,index1) in items.list" :key='index1'>
								<topic-list :item="item" :index="index1"></topic-list>
							</block>
						</view>
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
	import noThing from '../../components/common/noThing.vue'
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
		import topicList from '../../components/action/topicList.vue' //话题列表
	export default {
		components: {
			swiperTabHead,
			noThing,
			loadMore,
			topicList
		},
		data() {
			return {
				swiperHeight: 500, //可展示y方向滚动的区域的高度
				tabIndex: 0, //顶部选项切换变量
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
				newsList: [
					{
						loadText: '上拉加载更多',
						list: [{
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
							titlePic:"../../static/img/share1.gif",
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
						},
						{
							titlePic:"../../static/img/share1.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						}],
					},
					{
						loadText: '上拉加载更多',
						list: [{
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
						},{
							titlePic:"../../static/img/share1.gif",
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
						},{
							titlePic:"../../static/img/share1.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						},{
							titlePic:"../../static/img/share1.gif",
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
						},{
							titlePic:"../../static/img/share.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
						},],
					},
					{
						loadText: '上拉加载更多',
						list: [],
					},
					{
						loadText: '上拉加载更多',
						list: []
					},
					{
						loadText: '上拉加载更多',
						list: []
					},
					{
						loadText: '上拉加载更多',
						list: []
					},
					{
						loadText: '上拉加载更多',
						list: []
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
							titlePic:"../../static/img/share1.gif",
							title:'话题名称',
							desc:'话题描述',
							totalNum:50,
							todayNum:10
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
		}
	}
</script>

<style>
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
	.topic-view{
		padding: 0 20rpx;
	}
</style>
