<template>
	<view class="body">
		<uni-collapse>
			<block v-for="(item,index) in list" :key="index">
				<uni-collapse-item :title="item.title" :showAnimation="true">
					<text class="content" style="padding:10rpx 20rpx;">{{item.content}}</text>
				</uni-collapse-item>
			</block>
		</uni-collapse>
		<button type="primary" class="user-set-btn">提交</button>
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
						title: '客服什么时候上线？',
						content: '客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线客服什么时候上线'
					},
					{
						title: '忘记账号怎么办？',
						content: '忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办忘记账号怎么办'
					},
					{
						title: '忘记密码怎么办？',
						content: '忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办忘记密码怎么办'
					},
					{
						title: '怎么搜索/查找用户？',
						content: '查找用户查找用户查找用户查找用户查找用户查找用户查找用户查找用户查找用户查找用户'
					},
					{
						title: '怎么取关用户？',
						content: '怎么取关用户怎么取关用户怎么取关用户怎么取关用户怎么取关用户怎么取关用户怎么取关用户怎么取关用户'
					}
				]
			}
		},
		methods: {

		}
	}
</script>

<style scoped>
	@import "../../common/form.css";

	.body {
		padding: 0 20rpx;
	}
</style>
