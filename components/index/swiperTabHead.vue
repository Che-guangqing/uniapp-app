<template>
	<view class="">
		<view class="tabs">
			<scroll-view scroll-x class="scroll-h">
				<block v-for="(tab,index) in tabBars" :key="tab.id">
					<view class="uni-tab-item" @tap="ontabtap(index)">
						<text class="uni-tab-item-title" :class="tabIndex==index ? 'uni-tab-item-title-active' : ''">{{tab.name}}</text>
						<view :class="tabIndex==index ? 'swiper-tab-line' : ''"></view>
					</view>
				</block>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			tabBars:Array,
			tabIndex:Number
		},
		methods:{
			// tabbar点击切换事件
			ontabtap(index) {
				// 点击子组件 修父组件得值
				this.$emit('tabTap',index)
			},
		}
	}
</script>

<style scoped>
	.tabs {
		width: 100%;
		flex-direction: column;
		overflow: hidden;
		background-color: #ffffff;
		border-bottom: 1px solid #ccc;
		height: 100upx;
		box-sizing: border-box;
		/* #ifdef MP-ALIPAY || MP-BAIDU */
		height: 100upx;
		/* #endif */
	}
	
	.scroll-h {
		width: 750rpx;
		height: 100rpx;
		flex-direction: row;
		overflow-x: hidden;
		/* 	    #ifndef APP-PLUS */
		white-space: nowrap;
		/* #endif */
		/* flex-wrap: nowrap; */
		/* border-color: #cccccc;
		border-bottom-style: solid;
		border-bottom-width: 1px; */
	}
	
	.uni-tab-item {
		/* #ifndef APP-PLUS */
		display: inline-block;
		/* #endif */
		flex-wrap: nowrap;
		padding-left: 34rpx;
		padding-right: 34rpx;
	}
	
	.uni-tab-item-title {
		color: #969696;
		font-weight: block;
		font-size: 30rpx;
		height: 80rpx;
		line-height: 80rpx;
		flex-wrap: nowrap;
		/* #ifndef APP-PLUS */
		white-space: nowrap;
		/* #endif */
	}
	
	.uni-tab-item-title-active {
		color: #343434;
	}
	
	.swiper-tab-line {
		border-bottom: 6upx solid #fede33;
		border-top: 6upx solid #fede33;
		width: 60upx;
		margin: auto;
		border-radius: 20upx;
		transform: translateY(-20upx);
	}
	
</style>
