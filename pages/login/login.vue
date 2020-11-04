<template>
	<view>
		<!-- P107 占位组件 状态栏-->
		<view class="top"></view>
		<view class="icon iconfont icon-guanbi" @tap="back"></view>
		<!-- 登录输入框 -->
		<view class="body">
			<!-- 账号密码登录 -->
			<template v-if="!status">
				<input type="text" class="uni-input common-input" placeholder="昵称/手机号/邮箱" v-model="userName" />
				<view class="login-input-box">
				  <input type="text" class="uni-input common-input forget-input" placeholder="请输入密码" v-model="password" />
				  <view class="forget u-f-jsc-ac">忘记密码?</view>
				</view>
			</template>
			
			<!-- 手机验证码登录 -->
			<template v-else>
				<view class="login-input-box">
					<view class="phone u-f-jsc-ac">+86</view>
					<input type="text" class="uni-input common-input phone-input" placeholder="输入手机号码" v-model="phone" />
				</view>
				<view class="login-input-box">
				  <input type="text" class="uni-input common-input yanzheng-input" placeholder="请输入验证码" v-model="checkNum" />
				  <view class="yanzheng u-f-jsc-ac" @tap="getCheckNum">
					  <view class="yanzheng-text u-f-jsc-ac"> {{!codeTime?'获取验证码?':codeTime+'s' }} </view>
				  </view>
				</view>
			</template>

			
			<button type="primary" class="user-set-btn " :class="{'user-set-btn-disable':disabled}" @tap="submit" :disabled="disabled"
			 :loading="loading">登录</button>
		</view>
		<!-- 登录状态切换 -->
		<view class="login-status u-f-jsc-ac login-padding " @tap='changeStatus'>
			{{status ? '账号密码登录' : '手机验证码登录'}}<view class="icon iconfont icon-jinru login-font-color"></view>
		</view>
		<!-- 第三方登录 -->
		<view class="other-login-title u-f-jsc-ac login-padding login-font-color">第三方登录</view>
		<other-login></other-login>
		<!-- 协议 -->
		<view class="u-f-jsc-ac login-padding login-font-color">注册即代表您同意<view class="login-rule">《xxx协议》</view></view>
	</view>
</template>

<script>
	import otherLogin from '../../components/my/otherLogin.vue'
	export default {
		components:{
			otherLogin
		},
		data() {
			return {
				disabled: true,
				loading: false,
				status: false, // false:账号密码登录 true:手机验证码登录
				userName: "",
				password: "",
				phone: "",
				checkNum: "",
				codeTime:0 //验证码倒计时
			}
		},
		methods: {
			// 返回上一步
			back() {
				uni.navigateBack({
					delta:1
				})
			},
			// 登录
			submit() {
				if(!this.status) {
					// 账号密码登录
					
				}else{
					// 验证码登录
					// 验证手机号合法性
					if( !this.isPhone() ) {
						// 验证不通过
						uni.showToast({ title:'请输入正确的手机号码', icon:'none'})
						return
					}
				}
				console.log('提交登录')
			},
			// 切换登录状态
			changeStatus() {
				this.initInput()
				this.status = !this.status
			},
			// 改变登录按钮状态的方法
			onBtnChange() {
				if( (this.userName && this.password) || (this.phone && this.checkNum) ) {
					this.disabled = false;
					return
				}
				this.disabled = true
			},
			// 初始化表单
			initInput() {
				this.userName = ''
				this.password = ''
				this.phone = ''
				this.checkNum = ''
			},
			// 验证手机号码
			isPhone() {
				let mPattern = /^1[34578]\d{9}$/;
				return mPattern.test(this.phone)
			},
			// 获取验证码
			getCheckNum() {
				// 如果已经在获取 就不能再次获取
				if(this.codeTime > 0) {
					uni.showToast({ title:'不能重复获取', icon:'none'})
					return
				}
				// 验证手机号合法性
				if( !this.isPhone() ) {
					// 验证不通过
					uni.showToast({ title:'请输入正确的手机号码', icon:'none'})
					return
				}
				
				// 请求服务器，服务器发送验证码
				// 发送成功，开启倒计时
				this.codeTime = 10;
				let timer = setInterval(() => {
					this.codeTime --;
					if(this.codeTime < 1) {
						clearInterval(timer)
						this.codeTime = 0
					}
				}, 1000)
			}
		},
		watch:{
			userName(val) {
				this.onBtnChange()
			},
			password(val){
				this.onBtnChange()
			},
			phone(val) {
				this.onBtnChange()
			},
			checkNum(val) {
				this.onBtnChange()
			}
		}
	}
</script>

<style scoped>
	@import "../../common/form.css";
	.top{
		width: 100%;
		height: 300rpx;
		background-color: #FFE933;
	}
	.icon-guanbi{
		position: fixed;
		top: 60rpx;
		left: 30rpx;
		font-size: 50rpx;
		color: #332FOA;
	}
	/* body */
	.body {
		padding:40rpx 20rpx;
	}
	.login-input-box{
		position: relative;
	}
	.login-input-box input{
		
	}
	.forget{
		position: absolute;
		right: 0;
		top: 0;
		width: 150rpx;
		height: 100%;
		z-index: 1;
	}
	.forget-input{
		padding-right: 150rpx;
	}
	.phone{
		position: absolute;
		left: 0;
		top: 0;
		width: 100rpx;
		height: 100%;
		z-index: 1;
		font-weight: bold;
	}
	.phone-input{
		padding-left: 100rpx;
	}
	.yanzheng{
		position: absolute;
		right: 0;
		top: 0;
		width: 170rpx;
		height: 100%;
		z-index: 1;
		font-weight: bold;
	}
	.yanzheng-input{
		padding-right: 170rpx;
	}
	.yanzheng-text{
		width: 100%;
		height: 50rpx;
		background-color: #EEEEEE;
		border-radius: 10rpx;
		color: #BBBBBB;
	}
	.login-padding{
		padding: 20rpx 0;
	}
	.login-font-color{
		color: #CCCCCC;
	}
	.login-rule{
		color: #0A98D5;
	}
	.other-login-title:before{
		position: absolute;
		background-color: #CCCCCC;
		width: 100rpx;
		height: 1rpx;
		content: '';
		left: 25%;
	}
	.other-login-title:after{
		position: absolute;
		background-color: #CCCCCC;
		width: 100rpx;
		height: 1rpx;
		content: '';
		right: 25%;
	}
</style>
