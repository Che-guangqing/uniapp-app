<template>
	<view>
		<!-- 话题介绍 -->
		<topic-info :item="topicInfo"></topic-info>
		<!-- tab切换 -->
		<swiper-tab-head :tabBars="tabBars" :tabIndex="tabIndex" @tabTap='tabTap' scrollStyle="border-bottom: 0"
		 scrollItemStyle="width:50%"></swiper-tab-head>
		<!-- 列表 -->
		<view class="topic-detail-list">
			<block v-for="(item,index) in tabList" :key="index">
				<template v-if="tabIndex==index">
					<!-- 列表 -->
					<block v-for="(list,listIndex) in item.list" :key="listIndex">
						<common-list :item="list" :index="listIndex"></common-list>
					</block>
					<!-- 上拉加载 -->
					<load-more :loadText="item.loadText"></load-more>
				</template>
			</block>
		</view>
	</view>
</template>

<script>
	import topicInfo from '../../components/topic/topicInfo.vue'
	import swiperTabHead from '../../components/index/swiperTabHead.vue' //tabbar
	import commonList from '../../components/common/commonList.vue' // 公共列表
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	export default {
		data() {
			return {
				tabIndex: 0,
				tabBars: [{
						name: '默认',
						id: 'moren'
					},
					{
						name: '最新',
						id: 'zuixin'
					}
				],
				topicInfo: {
					titlePic: '../../static/img/head2.jpeg',
					title: '啦啦啦啦，啦啦啦',
					desc: '我是描述',
					totalNum: 793,
					todayNum: 45
				},
				tabList: [{
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
		components: {
			topicInfo,
			swiperTabHead,
			commonList,
			loadMore
		},
		methods: {
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
			// 下拉刷新
			getData() {
				// 获取数据
				setTimeout(() => {
					// 模拟获取数据
					let arr = [{
						userHead: '../../static/img/head1.jpg',
						userName: '昵称',
						sex: '女',
						age: 18,
						address: '陕西 西安',
						isGuanzhu: false,
						title: '啦啦啦啦啦啦',
						titlePic: '../../static/img/bg3.jpg',
						dianzan: 181,
						commentNum: 130,
						shareNum: 132,
						video: false,
						share: false
					}]
					// 赋值
					this.tabList[this.tabIndex].list = arr
					// 关闭下拉刷新
					// 关闭下拉刷新函数
					uni.stopPullDownRefresh()
				}, 2000)
			}
		},
		// 页面上拉触底事件处理函数
		onReachBottom() {
			this.loadMore()
		},
		// 监听用户下拉动作 下拉刷新
		onPullDownRefresh() {
			this.getData()
		}
	}
</script>

<style scoped>

</style>
