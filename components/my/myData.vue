<template>
	<view class="home-data u-f-ac">
		<block v-for="(item,index) in homeData" :key="index">
			<view class="u-f1 u-f-jsc-ac u-f-column">
				<view>{{item.num}}</view>{{item.name}}
			</view>
		</block>
	</view>
</template>

<script>
	export default {
		props: {
			homeData: Array
		}
	}
</script>

<style scoped>
	/* 数据 */
	.home-data {
		padding: 20rpx 40rpx;
		color: #989898;
	}

	.home-data>view>view {
		color: #000000;
		font-size: 32rpx;
	}
</style>
