<template>
	<view class="body">
		<input type="text" class="uni-input common-input" placeholder="输入需要绑定的邮箱" v-model="email" />
		<input type="text" password class="uni-input common-input" placeholder="输入密码" v-model="password" />

		<button type="primary" class="user-set-btn " :class="{'user-set-btn-disable':disabled}" @tap="submit" :disabled="disabled"
		 :loading="loading">完成</button>
		 <!-- P99 正则验证 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				email: '',
				password: '',
				disabled: true,
				loading: false
			}
		},
		watch: {
			email(val) {
				this.change()
			},
			password(val) {
				this.change()
			}
		},
		methods: {
			// 监听输入框
			change() {
				if (this.email && this.password) {
					// 有值 提交按钮解除禁用 可点击
					this.disabled = false
					return
				}
				this.disabled = true
			},
			// 验证
			check() {
				if (!this.email || this.email == '') {
					uni.showToast({
						title: '邮箱不能为空',
						icon: 'none'
					})
					return false
				}
				// 验证邮箱格式
				let ePattern = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/
				if(!ePattern.test(this.email)) {
					uni.showToast({
						title: '邮箱格式不正确',
						icon: 'none'
					})
					return false
				}
				
				if (!this.password || this.password == '') {
					uni.showToast({
						title: '密码不能为空',
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
