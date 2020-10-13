<template>
	<view class="load-more">{{loadText}}</view>
</template>

<script>
	export default {
		props:{
			loadText:String
		}
	}
</script>

<style scoped>
	/* 上拉加载更多 */
	.load-more {
		text-align: center;
		color: #aaaaaa;
		padding: 15upx 0;
	}
</style>
