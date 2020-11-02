<template>
	<view class="home-list-item u-f-jsb-ac" hover-class="home-list-hover" @tap="clickEvent">
		<view class="u-f-jsc-ac">
			<view v-if="item.icon" class="icon iconfont" :class="['icon-'+item.icon]"></view>{{item.name}}
		</view>
		<view class="icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods: {
			// 点击事件
			clickEvent() {
				switch (this.item.clickType) {
					case 'navigateTo': // 修改密码事件
						if (this.item.url) {
							uni.navigateTo({
								url: this.item.url
							})
						}
						break;
				}
				console.log('点击了',this.item.clickType ,this.item.url)
			}
		}
	}
</script>

<style scoped>
	.home-list-item {
		padding: 20rpx;
		border-top: 1rpx solid #f4f4f4;
		border-bottom: 1rpx solid #f4f4f4;
		color: #333333;
	}

	.home-list-item>view>view {
		margin-right: 15rpx;
	}

	.home-list-item>.icon-jinru {
		color: #CCCCCC;
	}

	.home-list-hover {
		background-color: #F4F4F4;
	}
</style>
