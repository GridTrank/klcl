<template>
	<view class="detail_wrap">
		<view class="swiper_wrap">
			<u-swiper
			    :list="list1"
				circular
				indicator
				:autoplay="false"
				height="180"
			>
			</u-swiper>
		</view>
		<view class="buy row jc-sb">
			<view class="title">
				限时抢购
			</view>
			<view class="time">
				距离抢购结束
			</view>
		</view>
		<view class="detail_info">
			<view class="info">
				<view class="row jc-sb top">
					<view class="t-left">
						<text class="p1">￥</text><text class="p2">299</text><text class="p1">起</text>
					</view>
					<view class="t-right">
						收藏
					</view>
				</view>
				<view class="desc">
					详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍详情介绍
				</view>
				
				
				
				<view class="tab-wrap">
					<view class="tab-item" v-for="(item,index) in 3" :key="index">
						描述
						
					</view>
				</view>
			</view>
			<view class="share row jc-sb">
				<view class="imgs-wrap row">
					<image class="s-img"  v-for="(item,index) in 5 " :key="index"  src="@/static/images/car2.png" mode="widthFix"></image>
				</view>
				<view class="s-btn">
					我要分享
				</view>
			</view>
			
			<view class="releated_wrap">
				<view class="title">
					相关产品
				</view>
				<view class="re_list">
					<view class="re_item row jc-sb" v-for="(item,index) in 3" :key="index">
						<image src="@/static/img1.png" class="c-img"></image>
						<view class="re_info row jc-sb">
							<view class="name_price">
								<view class="name twoHidden">
									名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称
								</view>
								<view class="price">
									<text class="p1">￥100</text>
									<text class="p2">￥100</text>
								</view>
							</view>
							<view class="buy_btn">
								抢购
							</view>
						</view>
					</view>
				</view>
				
			</view>
		</view>
		<u-sticky offset-top="10">
			<view class="nav_tab row">
				<view class="nav_item" v-for="(item,index) in navList" :key="index" :class="[{'active':activeIndex==index}]" @click="activeIndex=index">
					{{item.label}}
				</view>
			</view>
		</u-sticky>
		<view class="pro_info">
			<view class="pro_tit">
				{{activeIndex==1?'预约须知':'产品详情'}}
			</view>
		</view>
	</view>
	
	
</template>

<script>
	export default {
		data() {
			return {
				list1:[
					require('@/static/home1.png'),
					require('@/static/home1.png'),
					require('@/static/home1.png'),
				],
				navList:[
					{label:'产品详情',value:1},
					{label:'预定须知',value:2},
				],
				activeIndex:0
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped lang="scss">
.detail_wrap{
	min-height: 100vh;
	background-color: #efefef;
	.buy{
		padding: 30upx;
		background-color: $base-color;
	}
	.detail_info{
		
		padding: 20upx;
		.info{
			background-color: #fff;
			border-radius: 20upx;
			padding:30upx 20upx;
			.t-left{
				.p1{
					color: $base-color;
				}
				.p2{
					color: $base-color;
					font-size: 38upx;
					font-weight: 600;
				}
			}
			.desc{
				margin-top: 10upx;
				font-weight: 600;
				font-size: 38upx;
			}
			.tab-wrap{
				margin-top: 20upx;
				.tab-item{
					position: relative;
					padding-left: 50upx;
					&::after{
						content: '';
						display: block;
						position: absolute;
						width: 30upx;
						height: 6upx;
						background-color: $base-color;
						left: 0;
						top: 50%;
					}
				}
			}
		}
		.share{
			margin-top: 20upx;
			padding: 30upx;
			background-color: $base-color;
			border-radius: 20upx;
			.imgs-wrap{
				.s-img{
					width: 80upx;
					border-radius: 50%;
					margin-left: -20upx;
					&:first-child{
						margin-left: 0;
					}
				}
			}
			.s-btn{
				width: 150upx;
				height: 60upx;
				background-color: #fff;
				border-radius: 50upx;
				text-align: center;
				line-height: 60upx;
				font-size: 20upx;
			}
		}
		.releated_wrap{
			margin-top: 20upx;
			background-color: #fff;
			border-radius: 20upx;
			padding: 20upx;
			.title{
				color: #000;
				margin-top: 10upx;
				font-size: 38upx;
				font-weight: 600;
			}
			.re_list{
				margin-top: 20upx;
				.re_item{
					height: 250upx;
					border-bottom:2upx solid #efefef;
					&:last-child{
						border-bottom: none;
					}
					.c-img{
						width: 200upx;
						height: 200upx;
						border-radius: 20upx;
						margin-right: 20upx;
						flex-shrink: 0;
					}
					.re_info{
						.name_price{
							width: 70%;
							.price{
								margin-top: 30upx;
								.p1{
									color: $base-color;
									margin-right: 20upx;
									font-size: 36upx;
								}
								.p2{
									color: #ddd;
									font-size: 28upx;
									text-decoration: line-through;
								}
							}
						}
						.buy_btn{
							background-color: $base-color;
							width: 100upx;
							height: 50upx;
							border-radius: 30upx;
							text-align: center;
							line-height: 50upx;
							color: #fff;
							
						}
					}
				}
			}
		}
	}
	.nav_tab{
		margin-top: 24upx;
		background-color: #fff;
		height: 120upx;
		.nav_item{
			width: 50%;
			text-align: center;
			font-size: 34upx;
			color: #333;
			height: 100%;
			line-height: 120upx;
			&.active{
				color: $base-color;
				border-bottom: 6upx solid $base-color;
			}
		}
	}
	.pro_info{
		margin-top: 20upx;
		background-color: #fff;
		height: 3000upx;
		width: 100%;
		.pro_tit{
			text-align: center;
			width: 100%;
			color: #000;
			font-size: 40upx;
			font-weight: 600;
			padding: 30upx 0;
		}
	}
}
</style>
