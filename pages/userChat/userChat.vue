<template>
	<view>
		<scroll-view id="scrollView" scroll-y :scroll-top="scrollTop" :scroll-with-animation="true" :style="{height:style.contentHeight+'px'}">
			<!-- 聊天列表 -->
			<block v-for="(item,index) in list" :key="index">
				<user-chat-list :item="item" :index="index"></user-chat-list>
			</block>
		</scroll-view>
		<!-- 输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
	</view>
</template>

<script>
	import userChatBottom from '../../components/paper/userChatBottom.vue'
	import time from '../../common/time.js' // 时间转化
	import userChatList from '../../components/paper/userChatList.vue' //聊天列表
	export default {
		components: {
			userChatBottom,
			userChatList
		},
		data() {
			return {
				list: [],
				scrollTop: 0,
				style: {
					contentHeight: 0,
					itemH: 0
				}
			}
		},
		methods: {
			// 初始化参数
			initData() {
				try {
					const res = uni.getSystemInfoSync();
					// 窗口高度(px)-输入框gaodu(120rpx)
					// this.style.contentHeight = res.windowHeight - uni.upx2px(120)
					this.style.contentHeight = res.windowHeight - uni.upx2px(120)
					console.log(res.windowHeight)
				} catch (e) {}
			},
			// 让信息超出可视区域时至于底部
			pageToBottom() {
				// 获取节点信息
				let q = uni.createSelectorQuery()
				q.select('#scrollView').boundingClientRect()
				q.selectAll('.user-chat-item').boundingClientRect()
				q.exec((res) => {
					// console.log(JSON.stringify(res))
					// 获取聊天列表的所有高度
					res[1].forEach((ret) => {
						this.style.itemH += ret.height
					});
					// 内容信息超出可视区域
					if (this.style.itemH > this.style.contentHeight) {
						// 让信息实时至于底部
						this.scrollTop = this.style.itemH
					}
				})
			},
			// 发送信息
			submit(data) {
				console.log('当前输入的是', data)
				// 发送逻辑
				// 构建数据
				let now = new Date().getTime()
				let obj = {
					userPic: '../../static/img/head4.jpeg',
					isme: true, //是好友发的还是自己发的
					type: "text", // 类型
					data: data,
					time: now, // 时间戳 展示不同时间
					gstime: time.gettime.getChatTime(now, this.list[this.list.length - 1].time)
				}
				this.list.push(obj)
				this.pageToBottom()
			},
			// 获取聊天数据
			getdata() {
				let arr = [{
						userPic: '../../static/img/head2.jpeg',
						isme: false, //是好友发的还是自己发的
						type: "text", // 类型
						data: '啦啦啦啦啦啦',
						time: '1554970014', // 时间戳 展示不同时间
					},
					{
						userPic: '../../static/img/head4.jpeg',
						isme: true, //是好友发的还是自己发的
						type: "img", // 类型
						data: '../../static/img/bg.jpg',
						time: '1554970414', // 时间戳 展示不同时间
					},
				]
				for (let i = 0; i < arr.length; i++) {
					// 转化时间
					// arr[i].gstime = time.gettime.gettime(arr[i].time)
					arr[i].gstime = time.gettime.getChatTime(arr[i].time, i > 0 ? arr[i - 1].time : 0)
				}
				this.list = arr
			}
		},
		onLoad() {
			this.getdata()
			this.initData()
			// let s = '1604031516934'
			// let s2 = '1604031516934'
			// console.log(time.gettime.gettime(s))
			// console.log(time.gettime.gettime(s2))
		},
		onReady() {
			this.pageToBottom()
		}
	}
</script>

<style scoped>


</style>
