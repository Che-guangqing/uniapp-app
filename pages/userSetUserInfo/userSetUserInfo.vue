<template>
	<view class="body">
		<view class="user-set-userInfo-list u-f-jsb-ac">
			<view>头像</view>
			<view class="u-f-ac" @tap='changeImg'>
				<image class="userInfo-img" :src="userPic" mode="aspectFill" lazy-load></image>
				<view class="icon iconfont icon-bi"></view>
			</view>
		</view>
		<view class="user-set-userInfo-list u-f-jsb-ac">
			<view>昵称</view>
			<view class="u-f-ac">
				<input class="userInfo-input" type="text" v-model="userName" />
				<view class="icon iconfont icon-bi"></view>
			</view>
		</view>
		<view class="user-set-userInfo-list u-f-jsb-ac">
			<view>性别</view>
			<view class="u-f-ac" @tap="changeOne('sex')">
				<view class="userInfo-text">{{sex}}</view>
				<view class="icon iconfont icon-bi"></view>
			</view>
		</view>
		<view class="user-set-userInfo-list u-f-jsb-ac">
			<view>生日</view>
			<!-- 时间选择器 -->
			<picker mode="date" :value="birthday" :start="startDate" :end="endDate" @change="bindDateChange">
				<view class="u-f-ac">
					<view class="userInfo-text">{{birthday}}</view>
					<view class="icon iconfont icon-bi"></view>
				</view>
			</picker>
		</view>
		<view class="user-set-userInfo-list u-f-jsb-ac">
			<view>情感</view>
			<view class="u-f-ac" @tap="changeOne('qinggan')">
				<view class="userInfo-text">{{qinggan}}</view>
				<view class="icon iconfont icon-bi"></view>
			</view>
		</view>
		<view class="user-set-userInfo-list u-f-jsb-ac">
			<view>职业</view>
			<view class="u-f-ac" @tap="changeOne('job')">
				<view class="userInfo-text">{{job}}</view>
				<view class="icon iconfont icon-bi"></view>
			</view>
		</view>
		<view class="user-set-userInfo-list u-f-jsb-ac">
			<view>家乡</view>
			<!--自定义 三级地区选择器 -->
			<picker-address @change="change">
				<view class="u-f-ac">
					<view class="userInfo-text">{{address}}</view>
					<view class="icon iconfont icon-bi"></view>
				</view>
			</picker-address>
		</view>
		<button type="primary" class="user-set-btn" @tap="submit">完成</button>
	</view>
</template>

<script>
	let sex = ['不限', '男', '女', ]
	let qinggan = ['未婚', '已婚']
	let job = ['IT', '教师', '公务员']
	import pickerAddress from '../../components/common/pickerAddress/pickerAddress.vue'
	export default {
		components:{
			pickerAddress
		},
		data() {
			return {
				userPic: '../../static/img/head2.jpeg',
				userName: '车车',
				sex: '不限',
				qinggan: '未婚',
				job: 'IT',
				birthday: '2020-10-25',
				address:'陕西-西安'
			}
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		methods: {
			// 修改头像
			changeImg() {
				uni.chooseImage({
					count: 1,
					sizeType: ['compressed'], //可以指定是原图还是压缩图，默认二者都有
					success: (res) => {
						// this.userPic = res.tempFilePaths
						// console.log(JSON.stringify(res.tempFilePaths));
					}
				});
			},
			// 单列选择
			changeOne(val) {
				let arr = []
				switch (val) {
					case 'sex':
						arr = sex
						break;
					case 'qinggan':
						arr = qinggan
						break;
					case 'job':
						arr = job
						break;
				}
				uni.showActionSheet({
					itemList: arr,
					success: (res) => {
						switch (val) {
							case 'sex':
								this.sex = arr[res.tapIndex]
								break;
							case 'qinggan':
								this.qinggan = arr[res.tapIndex]
								break;
							case 'job':
								this.job = arr[res.tapIndex]
								break;
						}
						// console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
					}
				});
			},
			submit() {},
			// 时间选择器
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();

				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			},
			bindDateChange(e) {
				this.birthday = e.target.value
				console.log(e)
			},
			// 自定义 地区选择组件
			change(data) {
				this.address = data.data.join('-')
				console.log(data.data.join('-'))
			},
		}
	}
</script>

<style scoped>
	@import "../../common/form.css";

	.body {
		padding: 0 20rpx;
	}

	.user-set-userInfo-list {
		padding: 20rpx;
		border-bottom: 1rpx solid #F4F4F4;
	}

	.user-set-userInfo-list>view:first-child {
		font-size: 32rpx;
		font-weight: bold;
		color: #9b9b9b;
	}

	.userInfo-img {
		width: 80rpx;
		height: 80rpx;
		border-radius: 50%;
	}

	.userInfo-input {
		text-align: right;
		/* color: #9b9b9b; */
	}

	/* 	.userInfo-text {
		color: #9b9b9b;
	} */

	.icon-bi {
		margin-left: 20rpx;
		color: #9b9b9b;
	}
</style>
