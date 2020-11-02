<template>
	<view class="body">
		<input type="text" password class="uni-input common-input" placeholder="输入旧密码" v-model="oldPassword" />
		<input type="text" password class="uni-input common-input" placeholder="输入新密码" v-model="newPassword" />
		<input type="text" password class="uni-input common-input" placeholder="输入确认密码" v-model="renewPassword" />

		<button type="primary" class="user-set-btn " :class="{'user-set-btn-disable':disabled}" @tap="submit" :disabled="disabled"
		 :loading="loading">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				oldPassword: '',
				newPassword: '',
				renewPassword: '',
				disabled: true,
				loading: false
			}
		},
		watch: {
			oldPassword(val) {
				this.change()
			},
			newPassword(val) {
				this.change()
			},
			renewPassword(val) {
				this.change()
			},
		},
		methods: {
			// 监听输入框
			change() {
				if (this.oldPassword && this.newPassword && this.renewPassword) {
					// 有值 提交按钮解除禁用 可点击
					this.disabled = false
					return
				}
				this.disabled = true
			},
			// 验证
			check() {
				if (!this.oldPassword || this.oldPassword == '') {
					uni.showToast({
						title: '旧密码不能为空',
						icon: 'none'
					})
					return false
				}
				if (!this.newPassword || this.newPassword == '') {
					uni.showToast({
						title: '新密码不能为空',
						icon: 'none'
					})
					return false
				}
				if (!this.renewPassword || this.renewPassword == '') {
					uni.showToast({
						title: '确认密码不能为空',
						icon: 'none'
					})
					return false
				}
				if (this.newPassword !== this.renewPassword) {
					uni.showToast({
						title: '确认密码和新密码不一致',
						icon: 'none'
					})
					return false
				}
				return true
			},
			// 提交
			submit() {
				this.loading = true 
				this.disabled = true
				if (!this.check()) {
					this.loading = false
					this.disabled = false
					return
				}
				uni.showToast({
					title: '验证通过',
					icon: 'success'
				})
				this.loading = false
				this.disabled = false
			}
		}
	}
</script>

<style scoped>
	@import "../../common/form.css";

	.body {
		padding: 0 20rpx;
	}
</style>
