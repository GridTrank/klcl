<template>
	<view >
		<navbar  @onRightClick="onRightClick" :mysNavConfig="mysNavConfig">
			<view class="s-wrap row" slot="center1" @click="toSearch">
				<image src="@/static/images/search.png" class="icon-img"></image>
				<text>请输入</text>
			</view>
			<view class="search" slot="right">
				搜索
			</view>
		</navbar>
		<view class="index-top">
			<view class="index-bg">
				<u-swiper
				    :list="list1"
					circular
					indicator
					:autoplay="false"
					height="150"
				>
				</u-swiper>
			</view>
			
		</view>
		<view class="cate-wrap ">
			<view class="title row jc-sb">
				<view class="left row">
					<image class="f-img" src="@/static/images/home-fl.png" mode=""></image>
					<text click="l-txt">车型分类</text>
				</view>
				<view class="right row"  @click="navTo('/pagesA/carType/carType')">
					<text click="r-txt">更多</text>
					<u-icon name="arrow-right" size="13"></u-icon>
				</view>
			</view>
			<view class="model-wrap mt20">
				<swiper class="swiper" :indicator-dots="true" :autoplay="false"  indicator-active-color="#FF8D51">
					<swiper-item v-for="(item,index) in 3" class="row jc-sb swiper-item" :key="index" >
						<view class="swiper-item column" v-for="(e,i) in 4" :key="i">
							<image src="@/static/images/car2.png" class="c-img"></image>
							<text class="c-name">分类名称</text>
						</view>
					</swiper-item>
				</swiper>
			</view>
		</view>
		<view class="cate-wrap order ">
			<view class="title row jc-sb">
				<view class="left row">
					<image class="f-img" src="@/static/images/home-dd.png" mode=""></image>
					<text click="l-txt">最新订单</text>
				</view>
			</view>
			<view class="order-list mt20">
				
			</view>
		</view>
		
		<tabbar :activeIndexProp="0"></tabbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mysNavConfig:{
					isHome:false,
					navPadding:false,
					navFixed:true,
					bgColor:'#FB852D',
					// searchConfig:{
					// 	placeholder:'输入关键词搜索'
					// }
				},
				list1:[
					'http://asses.ytq.wiki/uploads/20221129/5dc95a3f153fefc865a1fb485536c24aqJ8pcKVwA0atGPHx.jpg',
					'http://asses.ytq.wiki/uploads/20221129/5dc95a3f153fefc865a1fb485536c24aqJ8pcKVwA0atGPHx.jpg',
					'http://asses.ytq.wiki/uploads/20221129/5dc95a3f153fefc865a1fb485536c24aqJ8pcKVwA0atGPHx.jpg',
				],
				cateList:[
					
				]
			};
		},
		mounted() {
			
		},
		onLoad() {
			 uni.setNavigationBarColor({
			    fontColor: "#ffffff", 
			})
			uni.hideTabBar()
		},
		onPullDownRefresh(res){
			setTimeout(()=>{
				uni.stopPullDownRefresh()
			},3000)
		},
		methods:{
			toSearch(){
				uni.navigateTo({
					url:'/pagesA/search/search'
				})
			},
			onRightClick(){
				this.toSearch()
				console.log('search')
			}
		}
	}
</script>

<style lang="scss" scoped>
.search{
	color: #fff;
}
.s-wrap{
	background-color: #fff;
	width: 81%;
	padding:16upx 24upx;
	border-radius: 32upx;
	color: #7F7F7F;
	font-size: 24upx;
	.icon-img{
		width: 28upx;
		height: 28upx;
		margin-right: 34upx;
	}
}

.index-top{
	background: linear-gradient(0deg, #FB852D, #FF8968);
	width: 100%;
	height: 430upx;
	border-radius: 0 0 35% 35%;
	.index-bg{
		padding:200upx 30upx 0 30upx;
	}
}
.cate-wrap{
	padding: 30upx;
	margin-top: 80upx;
	&.order{
		margin-top: 0upx;
	}
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
</style>
