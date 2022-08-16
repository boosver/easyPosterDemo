<template>
	<view class="content">
		<canvas id="poster" canvas-id="poster"></canvas>
		
		
		<canvas class="line" canvas-id="line" id="line"></canvas>
	</view>
</template>

<script>
	import easyposter from 'easyposter'
	import uCharts from '@qiun/ucharts'
	export default {
		data() {
			return {
				title: 'Hello',
				canvasImg:''
			}
		},
		onLoad() {
			this.init()
		},
		methods: {
			init() {
				this.$nextTick(async ()=>{
					const ctx = uni.createCanvasContext('poster')
		
					const ep = new easyposter({
					    ctx
					})
					
					const bgInfo = await ep.easyGetImageInfo('https://api.gkapay.com/media/demo/bg.png');

					ep.easyDrawImgCover(bgInfo, 0, 0, 340, 501);
					
					ep.easyRectangle(20,90,300,270,10,"#FFFFFF");
					
					ep.easyText('7384', 30, 135, 35, '#000000');
					
					ep.easyText('cal', 110, 135, 12, '#333333');
					
					ep.easyText('本次消耗', 50, 160, 12, '#333333');
					
					ep.easyText('斜杠生活', 35, 415, 18, '#000000');
					
					ep.easyText('生命不息 运动不止', 35, 435, 12, '#333333');
					
					const qrcodeInfo = await ep.easyGetImageInfo('https://api.gkapay.com/media/demo/qrcode.jpg');
					
					ep.easyDrawImgCover(qrcodeInfo, 230, 390, 80, 80);
					
					const lineCtx = uni.createCanvasContext('line')
					
					let uChartsConfig = {
						type: "area",
						context: lineCtx,
						width: 300,
						height: 181,
						categories: ["2016", "2017", "2018", "2019", '2020'],
						series: [{
								name: "成交量A",
								data: [1, 5, 23, 10, 29],
								legendText: ''
							},
					
						],
						
						animation: true,
						background: "#FFFFFF",
						color: ["#FA9371", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452",
							"#9A60B4", "#ea7ccc"
						],
						padding: [15, 10, 0, 15],
						legend: {
							show: false
						},
						xAxis: {
							disableGrid: true
						},
						yAxis: {
							gridType: "dash",
							dashLength: 2
						},
						extra: {
							area: {
								type: "curve",
								opacity: 1,
								addLine: true,
								width: 2,
								gradient: true
							}
						}
					}
					
					await ep.easyDrawChart(uCharts, 'line', uChartsConfig, {
						x: 15,
						y: 170,
						width: 300,
						height: 181
					})
					
					ep.easyDrawSaveImg({
					    canvasId: 'poster',
					    destWidth: 340,
					    destHeight: 501,
					}).then((canvasImg) => {
					    console.log(canvasImg)
						this.canvasImg = canvasImg;
						
					})
					

				})

				
				
			}
		}
	}
</script>

<style>
	#poster {
		
		width:340px;
		height:501px;
		text-align: center;
		margin:0px auto;
	}
	.line {
		width: 300px;
		height: 181px;
		position: fixed;
		top: -10000rpx;
		left: 0rpx;
	}
</style>
