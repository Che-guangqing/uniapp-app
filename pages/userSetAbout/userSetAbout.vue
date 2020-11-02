<template>
	<view class="body">
		<image src="../../static/img/timg.jpeg" mode="aspectFill"></image>
		<view class="banben u-f-jsc-ac">version 1.0.0</view>
		<uni-collapse>
			<block v-for="(item,index) in list" :key="index">
				<uni-collapse-item :title="item.title" :showAnimation="true">
					<text class="content" style="padding:10rpx 20rpx;">{{item.content}}</text>
				</uni-collapse-item>
			</block>
		</uni-collapse>
	</view>
</template>

<script>
	import uniCollapse from '../../components/uni-collapse/uni-collapse.vue'
	import uniCollapseItem from '../../components/uni-collapse-item/uni-collapse-item.vue'
	export default {
		components: {
			uniCollapse,
			uniCollapseItem
		},
		data() {
			return {
				list: [{
						title: '新版本监测？',
						content: '客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线'
					},
					{
						title: '糗事百科用户协议？',
						content: '忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办'
					}
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>

	.body {
		padding: 0 30rpx;
	}
	image{
		width: 100%;
		height: 400rpx;
	}
	.banben{
		padding: 40rpx 0;
		color: #E9E9E9;
		font-size: 30rpx;
	}
</style>

