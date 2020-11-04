<template>
	<view>
		<!-- 背景图 + 用户信息 -->
		<user-space-head :userinfo="userinfo"></user-space-head>
		<!-- P116 -->
	</view>
</template>

<script>
	import userSpaceHead from '../../components/userSpace/userSpaceHead.vue'
	export default {
		components: {
			userSpaceHead
		},
		data() {
			return {
				userinfo: {
					bgImg: 1,
					userPic:"../../static/img/head.jpg",
					userName:"车车",
					sex:'女',
					age:18,
					isGuanzhu:false
				}
			}
		},
		methods: {
		}
	}
</script>

<style scoped>
	.user-space-margin {
		margin: 15rpx 0;
	}
</style>
