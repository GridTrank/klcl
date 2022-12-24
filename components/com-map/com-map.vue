<template>
	<view :style='{"width":"100%","height": height + "rpx"}'>
		<map id="map" class="map" :scale="scale" :show-location="true" :longitude="info.location.lng"
			:latitude="info.location.lat" :markers="markers" :polyline="polyline" :enable-rotate="true">
			
		</map>
	</view>
</template>

<script>
	import config from '@/config'
	const QQMapWX = require('../../pagesB/chooseAddress/js/qqmap-wx-jssdk.min.js')
	const qqmapsdk = new QQMapWX({
		key: config.qqmapWxKey
	})
	let _mapCtx = null;
	export default {
		name: "com-map",
		props: {
			info: {
				type: Object,
				default: () => {
					return {
						location: {}
					}
				}
			},
			type:String,
			markers: {
				type: Array,
				default: () => {
					return [{
						latitude: 39.909,
						longitude: 116.39742,
						id: 1,
						width: 20,
						height: 20,
						iconPath: require('@/static/123.png')
					}, {
						latitude: 39.50,
						longitude: 116.39,
						id: 2,
						width: 20,
						height: 20,
						iconPath: require('@/static/123.png')
					}]
				}
			},
			posiType:{
				type:String,
				default:''
			},
			height: {
				type: [Number, String],
				default: 300
			},

		},
		data() {
			return {
				scale: 10,
				polyline: [],
				departureTime: 0
			};
		},
		mounted() {
			_mapCtx = uni.createMapContext('map');
		},
		watch:{
			info:{
				handler(val){
					this.init()
				},
				immediate:true
			}
		},
		methods: {
			init() {
				let info=this.info
				let from={}
				if(this.posiType=='start'){
					from={
						latitude:info.nowAddress.location.lat,
						longitude:info.nowAddress.location.lng
					}
				}else if(this.posiType=='dest'){
					from={
						latitude:info.startAddressObj.location.lat,
						longitude:info.startAddressObj.location.lng
					}
				}
				let	to={
					latitude:info.location.lat,
					longitude:info.location.lng
				}
				qqmapsdk.direction({
					mode: 'driving', //可选值：'driving'（驾车）  trucking 货车
					//from参数不填默认当前地址
					// latitude纬度    longitude 经度
					from:from,
					to:to,
					size: 4, // 车型 1: 微型车  2: 轻型车 3: 中型车 4: 重型车
					policy: 'LEAST_TIME', //'9',  //参考实时路况，高速优先，尽量躲避拥堵
					height: 4,
					width: 2.5,
					length: 13,
					weight: 6.8,
					axle_weight: 34,
					axle_count: 6,
					is_trailer: 1,
					success: (res,data) => {
						let distance = data[0].distance / 1000;
						console.log(1231,distance)
						if (distance > 500) {
							var scale = 2;
						} else if (distance > 200) {
							var scale = 7;
						} else if (distance > 100) {
							var scale =12;
						} else {
							var scale = 15;
						}
						console.log(scale);
						var ret = res;
						var coors = ret.result.routes[0].polyline,
							pl = [];
						//坐标解压（返回的点串坐标，通过前向差分进行压缩）
						var kr = 1000000;
						for (var i = 2; i < coors.length; i++) {
							coors[i] = Number(coors[i - 2]) + Number(coors[i]) / kr;
						}
						//将解压后的坐标放入点串数组pl中
						for (var i = 0; i < coors.length; i += 2) {
							pl.push({
								latitude: coors[i],
								longitude: coors[i + 1]
							})
						}
						this.polyline = [{
							points: pl,
							color: '#4AC37A',
							width: 5,
							arrowLine:true,
						}]
						this.scale = scale;
					}
				})
			},
			handleAngleFun(pl, k) {
				let lng_a = pl[pl.length - k].longitude
				let lat_a = pl[pl.length - k].latitude
				let lng_b = pl[pl.length - k + 1].longitude
				let lat_b = pl[pl.length - k + 1].latitude
				return this.getAngleFun(lng_a, lat_a, lng_b, lat_b)
			},
			handleAngleFun2(pl, k) {
				let lng_a = pl[k].longitude
				let lat_a = pl[k].latitude
				let lng_b = pl[k + 1].longitude
				let lat_b = pl[k].latitude
				return this.getAngleFun(lng_a, lat_a, lng_b, lat_b)
			},
			getAngleFun(lng_a, lat_a, lng_b, lat_b) {
				var a = (90 - lat_b) * Math.PI / 180;
				var b = (90 - lat_a) * Math.PI / 180;
				var AOC_BOC = (lng_b - lng_a) * Math.PI / 180;
				var cosc = Math.cos(a) * Math.cos(b) + Math.sin(a) * Math.sin(b) * Math.cos(AOC_BOC);
				var sinc = Math.sqrt(1 - cosc * cosc);
				var sinA = Math.sin(a) * Math.sin(AOC_BOC) / sinc;
				var A = Math.asin(sinA) * 180 / Math.PI;
				var res = 0;
				if (lng_b > lng_a && lat_b > lat_a) res = A;
				else if (lng_b > lng_a && lat_b < lat_a) res = 180 - A;
				else if (lng_b < lng_a && lat_b < lat_a) res = 180 - A;
				else if (lng_b < lng_a && lat_b > lat_a) res = 360 + A;
				else if (lng_b > lng_a && lat_b == lat_a) res = 90;
				else if (lng_b < lng_a && lat_b == lat_a) res = 270;
				else if (lng_b == lng_a && lat_b > lat_a) res = 0;
				else if (lng_b == lng_a && lat_b < lat_a) res = 180;
				return res - 90
			},
			vehicle(pl, rotate = 0) {
				// console.log(pl,rotate)
				this.startLat2 = pl.latitude
				this.startLng2 = pl.longitude
				if (this.item.status === 3) {
					this.marker.push({
						latitude: pl.latitude,
						longitude: pl.longitude,
						iconPath: require('@/static/123.png'),
						width: 20,
						height: 20,
						anchor: {
							x: 0.01,
							y: 0.5
						},
						rotate: rotate,
						label: { //为标记点旁边增加标签   //因背景颜色H5不支持
							content: '已出发' ,
							textAlign: 'left',
							fontSize: 14,
							height: '22px',
							padding: '8px',
							bgColor: '#5984FE',
							borderRadius: '4px',
							color: '#FFF',
							// label 位置
							anchorX: 40,
							anchorY: -40,
						}
					})
				}
			},
			getPercent(num, total) {
				num = parseFloat(num);
				total = parseFloat(total);
				// console.log(num, total)
				if (isNaN(num) || isNaN(total)) {
					return 0;
				}

				return total <= 0 ? 0 : Math.round(num / total);
			}
		},
	}
</script>

<style lang="scss">
	.map {
		width: 100%;
		height: 300rpx;
		position: relative;

		.map-center-icon {
			position: absolute;
			left: 50%;
			top: 50%;
			transform: translate(-50%, -50%);
			width: 52upx;
			height: 52upx;
		}
	}
</style>
