<template>
	<view class="body">
		<block v-for="(item,index) in list" :key="index">
			<my-list-item :item="item" :key="index"></my-list-item>
		</block>
		<button type="primary" class="user-set-btn">退出登录</button>
	</view>
</template>

<script>
	import myListItem from '../../components/my/myListItem.vue'
	export default {
		components: {
			myListItem
		},
		data() {
			return {
				list: [{
						name: '账号与安全',
						clickType: 'navigateTo',
						url: '../../pages/userSetRepassword/userSetRepassword'
					},
					{
						name: '绑定邮箱',
						clickType: 'navigateTo',
						url: '../../pages/userSetEmail/userSetEmail'
					},
					{
						name: '编辑资料',
						clickType: 'navigateTo',
						url: '../../pages/userSetUserInfo/userSetUserInfo'
					},
					{
						name: '小纸条',
						clickType: '',
						url: ''
					},
					{
						name: '清除缓存',
						clickType: 'clear',
						url: ''
					},
					{
						name: '意见反馈',
						clickType: 'navigateTo',
						url: '../../pages/userSetHelp/userSetHelp'
					},
					{
						name: '关于我们',
						clickType: 'navigateTo',
						url: '../../pages/userSetAbout/userSetAbout'
					}
				]
			}
		},
		methods: {

		}
	}
</script>

<style scoped>
	@import "../../common/form.css";
	.body {
		padding: 0 20rpx;
	}
</style>
