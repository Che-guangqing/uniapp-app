<template>
	<view class="warp">
		<!-- 操作菜单 -->
		<paper-left-popup 
		 :isShow="isShow"
		 @hide="hidePopup"
		 @addFriend="addFriend"
		 @clear="clear"
		>
		</paper-left-popup>
		<!-- 消息列表 -->
		<block v-for="(item,index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
		<!-- 上拉加载 -->
		<load-more :loadText="loadText"></load-more>
	</view>
</template>
<script>
	import paperList from '../../components/paper/paperList.vue'
	import loadMore from '../../components/common/loadMore.vue' //上拉加载更多
	import paperLeftPopup from '../../components/paper/paperLeftPopup.vue' //操作菜单
	export default {
		components: {
			paperList,
			loadMore,
			paperLeftPopup
		},
		data() {
			return {
				isShow: false,
				loadText: '上拉加载更多',
				list: [{
						userPic: '../../static/img/head3.jpg',
						userName: '昵称',
						time: '10:32',
						data: '我是消息',
						noReadNum: '12'
					},
					{
						userPic: '../../static/img/head.jpg',
						userName: '昵称',
						time: '13:02',
						data: '我是消息',
						noReadNum: '6'
					},
					{
						userPic: '../../static/img/head1.jpg',
						userName: '昵称',
						time: '20:45',
						data: '我是消息',
						noReadNum: '1'
					},
					{
						userPic: '../../static/img/head3.jpg',
						userName: '昵称',
						time: '20:45',
						data: '我是消息',
						noReadNum: '0'
					}, {
						userPic: '../../static/img/head.jpg',
						userName: '昵称',
						time: '13:02',
						data: '我是消息',
						noReadNum: '6'
					},
					{
						userPic: '../../static/img/head2.jpeg',
						userName: '昵称',
						time: '13:02',
						data: '我是消息',
						noReadNum: '6'
					},
					{
						userPic: '../../static/img/head.jpg',
						userName: '昵称',
						time: '20:45',
						data: '我是消息',
						noReadNum: '1'
					}, ,
					{
						userPic: '../../static/img/head3.jpg',
						userName: '昵称',
						time: '13:02',
						data: '我是消息',
						noReadNum: '6'
					},
					{
						userPic: '../../static/img/head1.jpg',
						userName: '昵称',
						time: '20:45',
						data: '我是消息',
						noReadNum: '1'
					},
				]
			}
		},
		methods: {
			// 获取数据
			getData() {
				setTimeout(() => {
					// 获取数据
					let arr = [{
						userPic: '../../static/img/head4.jpeg',
						userName: '昵称',
						time: '13:02',
						data: '我是消息',
						noReadNum: '12'
					}, {
						userPic: '../../static/img/head.jpg',
						userName: '昵称',
						time: '13:02',
						data: '我是消息',
						noReadNum: '6'
					}]
					// 赋值
					this.list = arr
					// 关闭下拉刷新
					uni.stopPullDownRefresh()
				}, 2000)
			},
			// 上拉加载更多
			loadMore() {
				if (this.loadText != '上拉加载更多') {
					return
				}
				// 修改数据
				this.loadText = '加载中...'
				// 获取数据
				setTimeout(() => {
					// 获取完成
					let obj = {
						userPic: '../../static/img/head.jpg',
						userName: '昵称',
						time: '13:02',
						data: '我是消息',
						noReadNum: '6'
					}
					this.list.push(obj)
					this.loadText = '上拉加载更多'
				}, 800)
				// this.loadText='没有数据啦'				
			},
			// 操作菜单
			addFriend() {
				console.log('加好友')
				this.hidePopup()
			},
			clear() {
				console.log('清除')
				this.hidePopup()
			},
			hidePopup() {
				this.isShow = false
			},
			showPopup() {
				this.isShow = true
			},
		},
		// 页面上拉触底事件处理函数
		onReachBottom() {
			this.loadMore()
		},
		// 监听下拉刷新
		onPullDownRefresh() {
			this.getData()
		},
		//监听导航按钮点击事件
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 0:
					// console.log("点击了左边")
					this.hidePopup()
					// 打开好友列表页面
					uni.navigateTo({
						url:"../userList/userList"
					})
					break;
				case 1:
					this.showPopup()
					// console.log("点击了右边")
					break;
			}
		}
	}
</script>

<style scoped>
	.warp {
		padding: 0 20rpx;
	}


</style>
