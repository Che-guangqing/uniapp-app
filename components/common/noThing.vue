<template>
	<view class="no-thing">
		<image class="default-img" src="../../static/img/noInfo.jpg" mode="widthFix"></image>
		<view class="no-text">这里什么都没有哦~</view>
	</view>
</template>

<script>
</script>

<style scoped>
	.no-thing{
		width: 100%;
		height: 100%;
		background-color: #FFFFFF;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.default-img{
		width: 60%;
		margin:150upx;
	}
	.no-text{
		font-size: 50upx;
		color: #999;
	}
</style>
