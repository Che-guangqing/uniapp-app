<template>
	<view>
		<detail-info :item="detail"></detail-info>
		<!-- 评论组件 P86 -->
		<!-- 评论输入框 P87 -->

		<!-- 分享 -->
		<more-share :show="shareShow" @togle="togle"></more-share>
	</view>
</template>

<script>
	import detailInfo from '../../components/index/detailInfo.vue'
	import moreShare from '../../components/common/moreShare.vue'
	export default {
		components: {
			detailInfo,
			moreShare
		},
		data() {
			return {
				shareShow:false,
				comment:{
					count:20,
					list:[]
				},
				detail: {
					userHead: '../../static/img/head4.jpeg',
					userName: '昵称',
					sex: '男',
					age: 25,
					address: '陕西 西安',
					isGuanzhu: false,
					title: '我是标题,略略略',
					titlePic: '../../static/img/bg1.jpg',
					morePic: ['../../static/img/bg1.jpg', '../../static/img/bg.jpg', '../../static/img/bg3.jpg'],
					dianzan: 181,
					commentNum: 130,
					shareNum: 132,
					video: false,
					share: false
				}
			}
		},
		methods: {
			// 初始化数据
			initData(obj) {
				// 修改窗口导航标题
				uni.setNavigationBarTitle({
					title: obj.title
				})
			},
			togle() {
				this.shareShow=!this.shareShow
			}
		},
		onLoad(e) {
			this.initData(JSON.parse(e.detailData))
			// console.log(JSON.parse(e.detailData))
		},
		// 监听导航按钮事件
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				console.log('分享')
				this.togle()
			}
		}
	}
</script>

<style>

</style>
