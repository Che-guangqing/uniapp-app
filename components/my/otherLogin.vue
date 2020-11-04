<template>
	<!-- 第三方登录 -->
	<view class="other-login u-f-jsc-ac">
		<block v-for="(item,index) in providerList" :key='index'>
			<view class="u-f-jsc-ac icon-warp" @tap="tologin(item)">
				<view class="icon iconfont  u-f-jsc-ac" :class="['icon-'+item.icon]"></view>
			</view>
		</block>
	<!-- 	<view class="u-f-jsc-ac icon-warp">
			<view class="icon iconfont icon-xinlangweibo u-f-jsc-ac"></view>
		</view>
		<view class="u-f-jsc-ac icon-warp">
			<view class="icon iconfont icon-QQ u-f-jsc-ac"></view>
		</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				providerList: []
			}
		},
		methods:{
			// 登录方法
			tologin(provider) {
				uni.login({
					provider: provider.id,
					// #ifdef MP-ALIPAY
					scopes: 'auth_user', //支付宝小程序需设置授权类型
					// #endif
					success: (res) => {
						console.log(JSON.stringify(res));
						console.log('login success:', res);
						// 更新保存在 store 中的登录状态
						// this.login(provider.id);
						console.log('登录成功,保存到本地存储，修改当前用户登录状态')
						// #ifdef MP-WEIXIN
						console.warn('如需获取openid请参考uni-id: https://uniapp.dcloud.net.cn/uniCloud/uni-id')
						uni.request({
							url: 'https://97fca9f2-41f6-449f-a35e-3f135d4c3875.bspapp.com/http/user-center',
							method:'POST',
							data: {
								action: 'loginByWeixin',
								params: {
									code: res.code,
									platform: 'mp-weixin'
								}
							},
							success(res) {
								console.log(res);
								if (res.data.code !== 0) {
									console.log('获取openid失败：', res.result.msg);
									return
								}
								uni.setStorageSync('openid', res.data.openid)
							},
							fail(err) {
								console.log('获取openid失败：', err);
							}
						})
						// #endif
					},
					fail: (err) => {
						console.log('login fail:', err);
					}
				});
			},
			// 获取第三方登录
			getLoginAuth() {
				uni.getProvider({
					service: 'oauth',
					success: (result) => {
						this.providerList = result.provider.map((value) => {
							let providerName = '';
							let icon =''
							switch (value) {
								case 'weixin':
									providerName = '微信登录';
									icon = 'weixin'
									break;
								case 'qq':
									providerName = 'QQ登录'
									icon = 'QQ'
									break;
								case 'sinaweibo':
									providerName = '新浪微博登录'
									icon = 'xinlangweibo'
									break;
								// case 'xiaomi':
								// 	providerName = '小米登录'
								// 	break;
								case 'alipay':
									providerName = '支付宝登录'
									icon = ''
									break;
								// case 'baidu':
								// 	providerName = '百度登录'
								// 	break;
								// case 'toutiao':
								// 	providerName = '头条登录'
								// 	break;
								// case 'apple':
								// 	providerName = '苹果登录'
								// 	break;
							}
							return {
								name: providerName,
								icon: icon,
								id: value
							}
						});
						
					},
					fail: (error) => {
						console.log('获取登录通道失败', error);
					}
				})
			}
		},
		onLoad() {
			this.getLoginAuth()
		}
	}
</script>

<style scoped>
	.other-login {
		padding: 20rpx 80rpx;
	}
	
	.icon-warp {
		flex: 1;
	}
	
	.icon-warp>.iconfont {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		font-size: 55rpx;
		color: #FFFFFF;
	}
	
	.icon-weixin {
		background-color: #2bd19b;
	}
	
	.icon-xinlangweibo {
		background-color: #fc7729;
	}
	
	.icon-QQ {
		background-color: #2caefc;
	}
</style>
