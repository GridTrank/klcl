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
					<view v-for="(item,index) in 3" :key="index">
						<view class="">
							描述
						</view>
					</view>
				</view>
			</view>
			<view class="share row jc-sb">
				<view class="imgs-wrap">
					
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
			padding: 20upx;
		}
	}
}
</style>
