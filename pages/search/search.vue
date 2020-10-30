<template>
	<view>
		<template v-if="list.length>0">
			<block v-for="(item,index) in list" :key="index">
				<index-list :item='item' :index='index'></index-list>
			</block>
			<!-- 上拉加载 -->
			<load-more :loadText="loadText"></load-more>
		</template>
		<template v-else-if="isSearch && list.length<1">
			<!-- 如果用户点击了搜索 并且搜索之后没有获取到数据 显示无内容的默认页 -->
			<no-thing></no-thing>
		</template>
	</view>
</template>

<script>
	import indexList from '../../components/index/indexList.vue'
	import noThing from '../../components/common/noThing.vue'
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	export default {
		components: {
			indexList,
			noThing,
			loadMore
		},
		data() {
			return {
				isSearch:false, //有没有搜索，
				loadText: '上拉加载更多',
				list: [],
				searchText:''
			}
		},
		methods: {
			// 搜索事件
			getdata() {
				uni.showLoading()
				// 请求服务器 post keyword:this.searchText
				setTimeout(() => {
					let arr = [
						{
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
					]
				    this.list=arr
					uni.hideLoading()
					this.isSearch=true
				}, 1000)

			},
			// 上拉加载
			loadMore(index) {
				if (this.loadText != '上拉加载更多') {
					return
				}
				// 修改数据
				this.loadText = '加载中...'
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
					this.list.push(obj)
					this.loadText = '上拉加载更多'
				}, 800)
				// this.loadText='没有数据啦'
				// 注意： 触底事件失效：scroll-view必须设置高度
			}

		},
		// 监听原生标题栏按钮点击事件，参数为Object
		onNavigationBarButtonTap(e) {
			// 取消按钮的index为0
			if (e.index == 0) {
				uni.navigateBack({
					delta: 1
				})
			}
			// console.log(JSON.stringify(e.index))
		},
		// 监听原生标题栏搜索输入框输入内容变化事件
		onNavigationBarSearchInputChanged(e) {
			console.log(e.text, '文本')
			this.searchText=e.text
		},
		// 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。
		onNavigationBarSearchInputConfirmed(e) {
			console.log(e.text, '搜索')
			if(e.text) {
				this.getdata()
			}
		},
		// 监听页面触底事件
		onReachBottom() {
			this.loadMore()
		},
		// 监听下拉刷新
		onPullDownRefresh() {
			this.getdata();
			// 关闭下拉刷新
			uni.stopPullDownRefresh()
		}
	}
</script>

<style scoped>

</style>
