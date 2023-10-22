<template>
	<view class="home-wrap">
		<view class="index-top">
			<view class="nav-wrap"  >
				<view class="s-wrap row" @click="toSearch">
					<image src="@/static/images/search.png" class="icon-img"></image>
					<text>请输入</text>
				</view>
				<view class="search" slot="right">
					搜索
				</view>
			</view>
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
			<view class="top_label row jc-sb">
				<view class="label"> 品质保障 </view>
				<view class="label"> 售后无忧 </view>
				<view class="label"> 甄选好惠 </view>
				<view class="label"> 能省能赚 </view>
			</view>
			
		</view>
		<view class="cate-wrap ">
			<view class="row cate-list">
				<view class="cate-item column" v-for="(item,index) in 8" :key="index">
					<image src="@/static/img1.png" class="c-img"></image>
					<text class="c-label">123</text>
				</view>
			</view>
			
			<view class="cate-swiper">
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
		<view class="buying-wrap">
			<view class="title">
				限时抢购
			</view>
			<scroll-view class="mt20" scroll-x="true" >
				<view class="buying-list">
					<view class="buying-item" v-for="(item,index) in 6" :key="index">
						<image src="@/static/home1.png" class="b-img"></image>
						<view class="name twoHidden">名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称</view>
						<view class="buy_info">
							<view class="price-wrap">
								<text class="p1">￥12</text>
								<text class="p2">￥12</text>
							</view>
							<view class="time">
								
							</view>
							<view class="buy">
								立即抢购
							</view>
						</view>
						
					</view>
				</view>
			</scroll-view>
		</view>
		<view class="buying-after row jc-sa">
			<view class="a-item">
				往期抢购
			</view>
			<view class="a-item">
				下期抢购
			</view>
			<view class="a-item">
				预约使用
			</view>
		</view>
		<view class="pd20">
			<u-swiper
			    :list="list1"
				circular
				indicator
				:autoplay="false"
				height="90"
			>
			</u-swiper>
		</view>
		
		
		<view class="con-box">
			<view class="con-top row jc-sb">
				<view class="title">
					标题 
				</view>
				<view class="more">
					查看更多
				</view>
			</view>
			<view class="list">
				<view class="item row jc-sb" v-for="(item,index) in 6" :key="index">
					<image src="../../static/home1.png" class="c-img"></image>
					<view class="info column jc-sb">
						<view class="name twoHidden">名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称</view>
						<view class="price">
							<text class="p1"> ￥123 </text>
							<text class="p1"> ￥123 </text>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="con-box box2">
			<view class="con-top row jc-sb">
				<view class="title">
					标题 
				</view>
				<view class="more">
					查看更多
				</view>
			</view>
			<view class="list">
				<view class="item col" v-for="(item,index) in 6" :key="index">
					<image src="../../static/home1.png" class="c-img"></image>
					<view class="info column jc-sb">
						<view class="name twoHidden">名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称</view>
						<view class="price">
							<text class="p1"> ￥123 </text>
							<text class="p1"> ￥123 </text>
						</view>
					</view>
				</view>
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
					navFixed:false,
					// searchConfig:{
					// 	placeholder:'输入关键词搜索'
					// }
				},
				list1:[
					require('@/static/home1.png'),
					require('@/static/home1.png'),
					require('@/static/home1.png'),
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
.home-wrap{
	min-height: 100vh;
	background-color: #fff;
	padding-bottom: 130upx;
}
.index-top{
	width: 100%;
	height: 530upx;
	background-color: red;
	background-image: url('@/static/bg2.png');
	// padding-top: 100upx;
	.nav-wrap{
		padding: 20upx;
	}
	.search{
		color: #fff;
	}
	.s-wrap{
		padding:16upx 24upx;
		border-radius: 32upx;
		font-size: 24upx;
		background-color: #fff;
		.icon-img{
			width: 28upx;
			height: 28upx;
			margin-right: 34upx;
		}
	}
	.index-bg{
		padding: 20upx;
	}
	.top_label{
		padding: 0 20upx;
		.label{
			color: #fff;
		}
	}
}
.cate-wrap{
	padding: 30upx;
	background-color: #fff;
	border-radius: 30upx;
	margin-top: -30upx;
	.cate-list{
		flex-wrap: wrap;
		justify-content: space-between;
	}
	.cate-item{
		margin-bottom: 20upx;
		.c-img{
			width: 150upx;
			height: 150upx;
		}
	}
	.cate-swiper{
		
	}
	
}
.buying-wrap{
	padding: 30upx;
	// background-image: url('@/static/bg2.png');
	background-color:rgba(225, 22, 22, 0.8);
	border-radius: 30upx;
	.title{
		color: #fff;
		font-size: 40upx;
		font-weight: 600;
		padding-left: 20upx;
		position: relative;
		&::after{
			display: block;
			content: "";
			position: absolute;
			width:10upx;
			height: 100%;
			background-color: #fff;
			left: 0;
			top: 0;
		}
	}
	.buying-list{
		display: flex;
		flex-wrap: nowrap;
		width: 100%;
		.buying-item{
			width: 260upx;
			display: inline-block;
			margin-right: 20upx;
			background-color: #fff;
			border-radius: 20upx;
			overflow: hidden;
			flex-shrink: 0;
			&:last-child{
				margin-right: 0;
			}
			.b-img{
				width: 260upx;
				height: 260upx;
			}
			.buy_info{
				padding: 20upx;
			}
		}
	}
	
}
.pd20{
		padding: 20upx;
	}
.con-box{
	background-color: rgba(25, 222, 22, 0.5);
	border-radius: 30upx;
	padding: 30upx 20upx;
	margin-top: 30upx;
	.list{
		margin-top: 30upx;
		.item{
			margin-bottom: 20upx;
			border-radius: 20upx;
			overflow: hidden;
			height: 200upx;
			.c-img{
				flex-shrink: 0;
				width: 400upx;
				height: 100%;
			}
			.info{
				height: 160upx;
				background-color: #fff;
				padding: 20upx;
				align-items: flex-start;
				
			}
		}
	}
	&.box2{
		.list{
			display: flex;
			align-items:center;
			justify-content: space-between;
			flex-wrap: wrap;
			.item{
				width: 48%;
				height: auto;
				flex-shrink: 0;
				.c-img{
					height: 200upx;
					width: 100%;
					display: block;
				}
			}
		}
	}
}
</style>
