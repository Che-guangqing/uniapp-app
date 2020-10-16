<template>
	<view>
		<!-- 自定义导航栏 -->
		<view class="nav-bar u-f-jsb-ac">
			<view class="icon iconfont icon-fanhui-xianxing" @tap="back"></view>
			<view class="u-f" @tap="changeLook">{{yinsi}}
			  <view class="icon iconfont icon-xialazhankai"></view>
			</view>
			<view class="" @tap="submit">发布</view>
		</view>
		<!-- 多行输入框 -->
		<view class="uni-textarea">
			<textarea class="content" v-model="text" placeholder="说一句话嘛~" />
		</view>
		<!-- 上传多图 -->
		<upload-images @upload = "upload"></upload-images>
		<!-- 弹出公告  -->
		<uni-popup type="middle">ddd</uni-popup>
	</view>
</template>

<script>
	// import uniNavBar from "../../components/nav-bar/nav-bar.nvue"
	import uploadImages from '../../components/common/uploadImages.vue'
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	// 隐私数据
	let changelook = ['所有人可见', '仅自己可见', '好友可见']
	export default {
		data() {
			return {
				isget:false, //返回的标识 第一次还未提示用户是否保存为草稿
				yinsi: '所有人可见',
				text: '',
				imageList:[],
				showpopup:true
			}
		},
		methods: {
			// 保存为草稿
			baocun() {
				uni.showModal({
					content:'是否要保存为草稿',
					cancelText:'不保存',
					confirmText:'保存',
					success: () => {
						if(res.confirm) {
							// 保存
							console.log('保存')
						}else{
							// 不保存
							console.log('不保存')
						}
						this.isget = true
						uni.navigateBack({
							delta:1
						})
					}
				})
			},
			// 监听返回事件 添加保存为草稿功能
			onBackPress() {
				// 如果无值
				if(!this.text && this.imageList.length<1) {return}
				// 如果有值 存草稿
				if(!this.isget) {
					// 第一次弹出提示
					this.baocun()
					return true; //阻止返回的默认事件
				}
			},
			// 返回
			back() {
				uni.navigateBack({
					delta:1
				})
			},
			// 发布
			submit() {
				console.log('发布')
				uni.showModal({
					title:'提示',
					content:'是否要发布？',
					success: (res) => {
						if(res.confirm) {
							console.log('发布内容')
						}
					}
				})
			},
			// 隐私
			changeLook() {
				console.log('隐私')
				uni.showActionSheet({
				    itemList: changelook,
				    success: (res) => {
				        // console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
						this.yinsi = changelook[res.tapIndex]
						console.log(res.tapIndex)
				    },
				})
			},
			// 上传图片组件中数据修改 要在此父组件进行监听
			upload(arr) {
				// console.log(arr)
				this.imageList = arr
			},
			// popup隐藏
			hidePopup() {}
			
		},
		components: {
			uploadImages,
			uniPopup
			// uniNavBar
		}
	}
</script>

<style scoped>
	.nav-bar{
		height: 100rpx;
		border-bottom: 5rpx solid #EEEEEE ;
		width: 95%;
		margin: 0 auto;
	}
	.uni-textarea{
		border: 1upx solid #EEEEEE 
	}


</style>
