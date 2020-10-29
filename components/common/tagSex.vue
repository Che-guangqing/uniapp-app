<template>
	<view>
		<!-- 此组件为公共列表组件中的性别年龄部分 -->
		<view class="icon-warp u-f-jsc-ac" :class="{'blue-icon':sex==='男','red-icon':sex==='女'}">
			<view :class="{'sex':true,'icon iconfont icon-nan':sex==='男','icon iconfont icon-nv':sex==='女'}"></view>
			{{age}}
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			sex: String,
			age: Number
		}
	}
</script>

<style scoped>
	.icon-warp {
		width: 72rpx;
		height: 32rpx;
		line-height: 32rpx;
		text-align: center;
		border-radius: 25rpx;
		/* margin-left: 20rpx; */
		color: #FFFFFF;
		font-size: 12rpx;
	}

	.blue-icon {
		background-color: #0A98D5;
	}
    .sex{
		font-size: 6rpx;
		margin-right: 5rpx;
	}
	.red-icon {
		background-color: #DD4A68;
	}
</style>
