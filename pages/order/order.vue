<template>
	<view class="order-wrap">
		<navbar  @onRightClick="onRightClick" :mysNavConfig="mysNavConfig">
			<view class="region row" slot="left" @click="toSelectRegion">
				{{city}}<u-icon name="arrow-down" color="#fff" size="16"></u-icon>
			</view>
			<view class="search" slot="right">
				搜索
			</view>
		</navbar>
		<view class="index-top">
			<u-swiper
			    :list="list1"
				circular
				indicator
				:autoplay="false"
				height="150"
			>
			</u-swiper>
		</view>
		<view class="filter-wrap">
			<view class="row">
				<view :class="['f-item' ,'row',{'active':filterActive===index}]" v-for="(item,index) in needList" @click="selectFilter(index)">
					{{item.label}}
					<image 
					:src="filterActive===index?require('@/static/images/icon1-a.png'):require('@/static/images/icon1.png')" 
					class="s-img ml10" >
					</image>
				</view>
			</view>
		</view>
		<view class="cate-wrap  ">
			<view class="order-list ">
				<view class="order-item " v-for="(item,index) in 5" :key="index">
					<orderList :info="item"></orderList>
				</view>
			</view>
		</view>
		<u-popup :show="showPop" @close="showPop=false" >
		    <view class="filter-pop">
				<view class="title row jc-sb model">
					<text class="f32-c333">{{fTitle}}</text>
					<u-icon name="close" size="13"></u-icon>
				</view>
				<view class="model item row jc-sb" v-for="(item,index) in filterList" :key="index" @click="selectFilterValue(item,index)">
					<text :class="['left','f28-c666',{'active':labelActive==index}]">{{item.label}}</text>
					<image 
					class="r-img" 
					:src="labelActive==index?require('@/static/images/xzs.png'):require('@/static/images/wxz.png')" >
					</image>
				</view>
				<view class="model btn" @click="submit">
					确定
				</view>
		    </view>
		</u-popup>
		<tabbar :activeIndexProp="3"></tabbar>
	</view>
</template>

<script>
	import config from '@/config'
	const QQMapWX = require('@/pagesB/chooseAddress/js/qqmap-wx-jssdk.min.js')
	const qqmapsdk = new QQMapWX({
		key: config.qqmapWxKey
	})
	export default {
		data() {
			return {
				mysNavConfig:{
					isHome:false,
					navPadding:true,
					navFixed:true,
					bgColor:'#FB852D',
					searchConfig:{
						placeholder:'输入关键词搜索'
					}
				},
				city:'',
				list1:[
					'http://asses.ytq.wiki/uploads/20221129/5dc95a3f153fefc865a1fb485536c24aqJ8pcKVwA0atGPHx.jpg',
					'http://asses.ytq.wiki/uploads/20221129/5dc95a3f153fefc865a1fb485536c24aqJ8pcKVwA0atGPHx.jpg',
					'http://asses.ytq.wiki/uploads/20221129/5dc95a3f153fefc865a1fb485536c24aqJ8pcKVwA0atGPHx.jpg',
				],
				cateList:[],
				needList:[
					{label:'需求筛选'},
					{label:'车型'},
					{label:'里程'},
					{label:'时间'},
				],
				filterModel:{
					val1:'',
				},
				filterList:[
					{label:'综合排序',value:1},
					{label:'最新优先',value:2},
					{label:'距离优先',value:3},
				],
				labelActive:0,
				fTitle:'需求筛选',
				filterActive:0,
				showPop:false
			};
		},
		mounted() {
			
		},
		onLoad() {
			this.getLocation()
		},
		methods:{
			getLocation(){
				uni.getLocation({
					type: 'gcj02',
					success: res=> {
						const { latitude, longitude } = res
						qqmapsdk.reverseGeocoder({
							location: latitude ? `${latitude},${longitude }` : '',
							sig: config.qqmapWxKey, // 这个sig就是上面要准备的第二项SK
							success: (val) => {
								this.city=val.result.ad_info.city
							},
							fail: (err) => {
								console.log('获取城市失败')
							}
						})
					}
				})
			},
			selectFilter(index){
				this.filterActive=index
				this.fTitle=this.needList[index].label
				this.labelActive=0
				switch(index){
					case 0:
						this.filterList=[
							{label:'综合排序',value:1},
							{label:'最新优先',value:2},
							{label:'距离优先',value:3},
						]
						break;
					case 1:
						this.filterList=[
							{label:'货车',value:1},
							{label:'卡车',value:2},
							{label:'客车',value:3},
						]
						break;
					case 2:
						this.filterList=[
							{label:'10km',value:1},
							{label:'20km',value:2},
							{label:'30km',value:3},
						]
						break;
					case 3:
						this.filterList=[
							{label:'最新发布',value:1},
							{label:'6月29日',value:2},
							{label:'6月28日',value:3},
						]
						break;
				}	
				this.showPop=true
			},
			selectFilterValue(item,index){
				this.labelActive=index
			},
			toSearch(){
				uni.navigateTo({
					url:'/pagesA/search/search'
				})
			},
			onRightClick(){
				this.toSearch()
			},
			toSelectRegion(){
				uni.navigateTo({
					url:'/pagesB/chooseAddress/cityList'
				})
			},
			submit(){
				
			}
		}
	}
</script>

<style lang="scss" scoped>
.search{
	color: #fff;
}
.region{
	color: #fff;
	font-size: 28upx;
}
.index-top{
	padding: 30upx;
}
.filter-wrap{
	padding: 25upx;
	background-color: #fff;
	border-bottom: 2upx solid #ddd;
	margin-bottom: -20upx;
	.f-item{
		position: relative;
		margin-right: 50upx;
		align-items: baseline;
		.s-img{
			width: 12upx;
			height: 12upx;
		}
		&.active{
			color: $base-color;
		}
	}
}
.cate-wrap{
	.title{
		.left{
			.f-img{
				width: 38upx;
				height: 38upx;
				margin-right: 12upx;
			}
			.l-txt{
				color: #333333;
				font-size: 32upx;
				font-weight: bold;
			}
		}
		.right{
			color: #999999;
			font-size: 26upx;
		}
	}
	.swiper{
		height: 200upx;
		/deep/ swiper-item{
			height: 75% !important;
		}
		.swiper-item{
			.c-img{
				width: 107upx;
				height: 107upx;
			}
			.c-name{
				color: #333333;
				font-size: 26upx;
			}
		}
	}
	.order-list{
		padding-bottom: 200upx;
	}
	
}
.filter-pop{
	.model{
		padding: 30upx;
		border-bottom: 2upx solid #E5E5E5;
		&.item{
			.r-img{
				width: 38upx;
				height: 38upx;
			}
			.left.active{
				color: $base-color;
			}
		}
		&.btn{
			border: none;
			text-align: center;
			background-color: $base-color;
			color: #fff;
			
		}
	}
}
</style>
