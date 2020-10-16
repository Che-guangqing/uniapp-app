<template>
	<view>
		搜索页
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		},
		// 监听原生标题栏按钮点击事件，参数为Object
		onNavigationBarButtonTap(e) {
			// 取消按钮的index为0
			if(e.index == 0) {
				uni.navigateBack({
					delta:1
				})
			}
			// console.log(JSON.stringify(e.index))
		},
		// 监听原生标题栏搜索输入框输入内容变化事件
		onNavigationBarSearchInputChanged(e) {
			console.log(e.text,'文本')
		},
		// 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。
		onNavigationBarSearchInputConfirmed(e) {
			console.log(e.text,'搜索')
		}
	}
</script>

<style>

</style>
