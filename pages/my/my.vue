<template>
	<view>
		<!-- 未登录 -->
		<template v-if="!isLogin">
			<view class="u-f-jsc-ac">登录之后，体验更多功能</view>
			<!-- 第三方登录 -->
			<other-login></other-login>
			<!-- 账号密码登录 -->
			<view class="u-f-jsc-ac" @tap='openLogin'>
				<view>账号密码登录</view>
				<view class="icon iconfont icon-jinru"></view>
			</view>
		</template>
		
		<!-- 已登录 -->
		<template v-else>
			<my-info :homeInfo='homeInfo'></my-info>
		</template>

		<!-- 数据 -->
		<my-data :homeData="homeData"></my-data>
		<!-- 广告位 -->
		<view class="home-adv u-f-jsc-ac">
			<image src="//ossweb-img.qq.com/upload/webplat/info/yxzj/20190305/58993377293822.jpg" mode="" lazy-load></image>
		</view>
		<!-- 功能列表 -->
		<view class="home-list">
			<block v-for="(item,index) in list" :key="index">
				<my-list-item :item="item" :key="index"></my-list-item>
			</block>
		</view>
	</view>
</template>

<script>
	import myListItem from '../../components/my/myListItem.vue'
	import myInfo from '../../components/my/myInfo.vue'
	import otherLogin from '../../components/my/otherLogin.vue'
	import myData from '../../components/my/myData.vue'
	export default {
		components:{
			myListItem,
			myInfo,
			otherLogin,
			myData
		},
		data() {
			return {
				isLogin:false,
				homeInfo:{ // 已登录信息
					userPic:'../../static/img/head1.jpg',
					userName:'名称',
					totalNum:0,
					todayNum:0
				},
				homeData:[
					{ name:'糗事',num:0 },
					{ name:'动态',num:0 },
					{ name:'评论',num:0 },
					{ name:'收藏',num:0 },
				],
				list:[ // 列表
					{ name:'浏览历史',icon:'liulan',clickType:'',url:''},
					{ name:'糗百认证',icon:'huiyuanvip',clickType:'',url:''},
					{ name:'审核糗事',icon:'keyboard1',clickType:'',url:''}
				]
			}
		},
		methods: {
			openLogin() {
				uni.navigateTo({
					url:'../login/login'
				})
			}
		},
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				console.log('点击了mene图标，跳转到设置页')
				uni.navigateTo({
					url:'../userSet/userSet'
				})
			}
		}
	}
</script>

<style scoped>

	
	




	/* adv */
	.home-adv {
		padding: 20rpx;
	}

	.home-adv>image {
		height: 150rpx;
		border-radius: 25rpx;
	}

	/* 功能列表 */
	.home-list {
		padding: 20rpx;
	}


</style>
