<template>
	<view class="qiun-columns">
		<view class="qiun-bg-white qiun-title-bar qiun-common-mt">
			<view class="qiun-title-dot-light">环形图</view>
		</view>
		<view class="qiun-charts">
			<canvas canvas-id="canvasRing" id="canvasRing" class="charts" @touchstart="touchRing"></canvas>
		</view>
	</view>
</template>
<script>
	import uCharts from '../../components/u-charts/u-charts.min.js';
	var _self;
	var canvaRing = null;
 
	export default {
		data() {
			return {
				cWidth: '',
				cHeight: '',
				pixelRatio: 1,
				serverData: '',
			}
		},
		onLoad() {
			_self = this;
			this.cWidth = uni.upx2px(750);
			this.cHeight = uni.upx2px(500);
			// this.getServerData();
			this.showRing('canvasRing')
		},
		methods: {
            // 这是官网给的调接口渲染数据的代码，我写的没有后台数据，自己写的固定的数据  就注销了
			// getServerData() {
			// 	// uni.request({
			// 	// 	url: 'https://www.ucharts.cn/data.json',
			// 	// 	data: {},
			// 	// 	success: function(res) {
			// 	// 		console.log(res.data.data)
			// 	// 		let Ring = {
			// 	// 			series: []
			// 	// 		};
			// 	// 		//这里我后台返回的是数组，所以用等于，如果您后台返回的是单条数据，需要push进去
			// 	// 		Ring.series = res.data.data.Ring.series;
			// 	// 		_self.showRing("canvasRing", Ring);
			// 	// 	},
			// 	// 	fail: () => {
			// 	// 		_self.tips = "网络错误，小程序端请检查合法域名";
			// 	// 	},
			// 	// });
			// },
			showRing(canvasId) {
				var chartData = {
					series :[{
						"name": "禁停路段",
						"data": 32
					  }, {
						"name": "交叉路口/铁路道口停车",
						"data": 17
					  }, {
						"name": "交叉路口/铁路道口停车",
						"data": 21
					  }, {
						"name": "其他",
						"data": 9
					  }]
				};
				canvaRing = new uCharts({
					$this: _self,
					canvasId: canvasId,
					type: 'ring',
					fontSize: 11,
					// legend: false,
					// title: {
					// 	name: '70%',
					// 	color: '#7cb5ec',
					// 	fontSize: 25 * _self.pixelRatio,
					// 	offsetY: 0 * _self.pixelRatio,  //这个调节字在中间圆的位置  中间没有字的就整个title注销
					// },
					// subtitle: {
					// 	name: '收益率',
					// 	color: '#666666',
					// 	fontSize: 15 * _self.pixelRatio,
					// 	offsetY: 5 * _self.pixelRatio,  // 这个调节字在中间圆的位置  中间没有字的就整个subtitle注销
					// },
					extra: {
						pie: {
							offsetAngle: -45,
							ringWidth: 20 * _self.pixelRatio,
							labelWidth: 15,
							border: true,
							borderWidth: 5
						}
					},
					background: '#fff',   // 中间圆的背景颜色
					pixelRatio: _self.pixelRatio,
					series: chartData.series,
					animation: true,     // 动画  画个圆的那种
					width: _self.cWidth * _self.pixelRatio,
					height: _self.cHeight * _self.pixelRatio,
					disablePieStroke: true,
					dataLabel: false,    //  图上红圈圈出来的线  true 显示
					legend: {
						show: false,
					}
				});
			},
			touchRing(e) {
				canvaRing.showToolTip(e, {
					format: function(item) {
						return item.name + ':' + item.data
					}
				});
			},
		}
	}
</script>
 
<style>
	page {
		background: #F2F2F2;
		width: 750upx;
		overflow-x: hidden;
	}
 
	.qiun-padding {
		padding: 2%;
		width: 96%;
	}
 
	.qiun-wrap {
		display: flex;
		flex-wrap: wrap;
	}
 
	.qiun-rows {
		display: flex;
		flex-direction: row !important;
	}
 
	.qiun-columns {
		display: flex;
		flex-direction: column !important;
	}
 
	.qiun-common-mt {
		margin-top: 10upx;
	}
 
	.qiun-bg-white {
		background: #FFFFFF;
	}
 
	.qiun-title-bar {
		width: 96%;
		padding: 10upx 2%;
		flex-wrap: nowrap;
	}
 
	.qiun-title-dot-light {
		border-left: 10upx solid #0ea391;
		padding-left: 10upx;
		font-size: 32upx;
		color: #000000
	}
 
	.qiun-charts {
		width: 750upx;
		height: 500upx;
		background-color: #FFFFFF;
	}
 
	.charts {
		width: 750upx;
		height: 500upx;
		background-color: #FFFFFF;
	}
</style>