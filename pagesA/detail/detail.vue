<template>
	<view class="detail_wrap">
		<view class="swiper_wrap">
			<u-swiper :list="(productInfo.commodityDetails || []).map(item=>item.imgPreviewUrl)" circular indicator
				:autoplay="false" height="180">
			</u-swiper>
		</view>
		<view class="buy row jc-sb" v-if="productInfo.flashSale == 1">
			<view class="title">
				限时抢购
			</view>
			<view class="time">
				<text v-if="status == 0">距离抢购结束</text>
				<text v-if="status == 1">距离开抢</text>
				<text v-if="status == 2">抢购已结束</text>
				<liu-countdown v-if="status != 2" :auto="true" ref="countdown" mode="4" :endDate="getTime()">
				</liu-countdown>
			</view>
		</view>
		<view class="detail_info">
			<view class="info">
				<view class="row jc-sb top">
					<view class="t-left">
						<text class="p1">￥</text><text
							class="p2">{{productInfo.price || productInfo.rushPurchasePrice}}</text><text
							class="p1">起</text>
					</view>
					<view class="t-right">
						收藏
					</view>
				</view>
				<view class="desc">
					{{productInfo.title}}
				</view>



				<!-- <view class="tab-wrap">
					<view class="tab-item" v-for="(item,index) in 3" :key="index">
						{{productInfo.remarks}}
						
					</view>
				</view> -->
			</view>
			<view class="share row jc-sb">
				<view class="imgs-wrap row">
					<image class="s-img" v-for="(item,index) in 5 " :key="index" src="@/static/images/car2.png"
						mode="widthFix"></image>
				</view>
				<view class="s-btn">
					我要分享
				</view>
			</view>

			<!-- <view class="releated_wrap">
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

			</view> -->
		</view>
		<u-sticky offset-top="10">
			<view class="nav_tab row">
				<view class="nav_item" v-for="(item,index) in navList" :key="index"
					:class="[{'active':activeIndex==item.value}]" @click="tabChange(item)">
					{{item.label}}
				</view>
			</view>
		</u-sticky>
		<view class="pro_info">
			<view class="pro_tit">
				<rich-text :nodes="productInfo.bookingInstructions" v-if="activeIndex"></rich-text>
				<rich-text :nodes="productInfo.details" v-else></rich-text>
			</view>
		</view>
		<div class="tab-bar row">
			<view class="icon" @click="toTab('/pages/home/home')">
				<image src="@/static/home.png" mode="heightFix"></image>
				<view>首页</view>
			</view>
			<view class="icon" @click="toTab('/pages/user/user')">
				<image src="@/static/user.png" mode="heightFix"></image>
				<view>我的</view>
			</view>
			<view class="icon">
				<image src="@/static/share.png" mode="heightFix"></image>
				<view>海报</view>
			</view>
			<button class="btn" @click="showPop=true" v-if="status == 0">立即预定</button>
			<button class="btn" v-else-if="status == 1">即将开抢</button>
			<button class="btn" v-else-if="status == 2">已结束</button>
		</div>
		<u-popup :show="showPop">
			<view class="sku-wrap">
				<view class="sku-title">
					<view class="btn close" @click="showPop = false">关闭</view>
					<view class="title">选择购买的产品</view>
					<view class="btn enter">确定</view>
				</view>
				<view class="sku-list">
					<u-radio-group v-model="productSku" placement="column">
						<u-radio :customStyle="{marginBottom: '8px'}"
							v-for="(item, index) in productInfo.commodityComboList" :key="index"
							:label="item.price +'元-' +item.comboName" :name="item.commodityId">
						</u-radio>
					</u-radio-group>
				</view>
			</view>
		</u-popup>
	</view>



</template>

<script>
	export default {
		data() {
			return {
				productSku: '',
				showPop: false,
				list1: [
					require('@/static/home1.png'),
					require('@/static/home1.png'),
					require('@/static/home1.png'),
				],
				navList: [{
						label: '产品详情',
						value: 0
					},
					{
						label: '预定须知',
						value: 1
					},
				],
				activeIndex: 0,
				productInfo: {},
				status: 0
			}
		},
		onLoad(options) {
			this.getData(options.id)
		},
		methods: {
			getTime() {
				const start = new Date(this.productInfo.startDate).getTime();
				const now = new Date().getTime();
				const end = new Date(this.productInfo.cutoffDate).getTime();
				if (start > now) {
					this.status = 1
					return this.productInfo.startDate
				} else if (end < now) {
					this.status = 2
					return this.productInfo.cutoffDate
				} else {
					this.status = 0
					return this.productInfo.cutoffDate
				}
			},
			getData(id) {
				this.$http(`/my-merchandise/commodity/info/${id}`).then(res => {
					this.productInfo = res.result
				})
			},
			tabChange(item) {
				this.activeIndex = item.value
			},
			toTab(url) {
				if (url == '/pages/user/user') {
					if (this.$util.isLogin()) {
						uni.switchTab({
							url,
						})
					}
				}
				uni.switchTab({
					url
				})
			}
		}
	}
</script>

<style scoped lang="scss">
	.detail_wrap {
		min-height: 100vh;
		background-color: #efefef;
		padding-bottom: 100upx;

		.buy {
			padding: 30upx;
			background-color: $base-color;
		}

		.detail_info {

			padding: 20upx;

			.info {
				background-color: #fff;
				border-radius: 20upx;
				padding: 30upx 20upx;

				.t-left {
					.p1 {
						color: $base-color;
					}

					.p2 {
						color: $base-color;
						font-size: 38upx;
						font-weight: 600;
					}
				}

				.desc {
					margin-top: 10upx;
					font-weight: 600;
					font-size: 38upx;
				}

				.tab-wrap {
					margin-top: 20upx;

					.tab-item {
						position: relative;
						padding-left: 50upx;

						&::after {
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

			.share {
				margin-top: 20upx;
				padding: 30upx;
				background-color: $base-color;
				border-radius: 20upx;

				.imgs-wrap {
					.s-img {
						width: 80upx;
						border-radius: 50%;
						margin-left: -20upx;

						&:first-child {
							margin-left: 0;
						}
					}
				}

				.s-btn {
					width: 150upx;
					height: 60upx;
					background-color: #fff;
					border-radius: 50upx;
					text-align: center;
					line-height: 60upx;
					font-size: 20upx;
				}
			}

			.releated_wrap {
				margin-top: 20upx;
				background-color: #fff;
				border-radius: 20upx;
				padding: 20upx;

				.title {
					color: #000;
					margin-top: 10upx;
					font-size: 38upx;
					font-weight: 600;
				}

				.re_list {
					margin-top: 20upx;

					.re_item {
						height: 250upx;
						border-bottom: 2upx solid #efefef;

						&:last-child {
							border-bottom: none;
						}

						.c-img {
							width: 200upx;
							height: 200upx;
							border-radius: 20upx;
							margin-right: 20upx;
							flex-shrink: 0;
						}

						.re_info {
							.name_price {
								width: 70%;

								.price {
									margin-top: 30upx;

									.p1 {
										color: $base-color;
										margin-right: 20upx;
										font-size: 36upx;
									}

									.p2 {
										color: #ddd;
										font-size: 28upx;
										text-decoration: line-through;
									}
								}
							}

							.buy_btn {
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

		.nav_tab {
			margin-top: 24upx;
			background-color: #fff;
			height: 120upx;

			.nav_item {
				width: 50%;
				text-align: center;
				font-size: 34upx;
				color: #333;
				height: 100%;
				line-height: 120upx;

				&.active {
					color: $base-color;
					border-bottom: 6upx solid $base-color;
				}
			}
		}

		.sku-wrap {

			.sku-title {
				height: 100upx;
				display: flex;
				width: 100%;

				.title {
					font-weight: 600;
					font-size: 36upx;
					flex: 2;
					display: flex;
					justify-content: center;
					align-items: center;
				}

				.btn {
					font-size: 30upx;
					padding: 0 20upx;
					height: 100%;
					line-height: 100upx;

					&.enter {
						color: #FB852F;
					}

					&.close {
						color: #999;
					}
				}
			}

			.sku-list {
				padding: 20upx;
				height: 500upx;
				overflow: auto;
			}
		}

		.tab-bar {
			z-index: 1000;
			height: 100upx;
			background-color: #fff;
			position: fixed;
			width: 100%;
			bottom: 0;
			left: 0;
			box-sizing: border-box;
			padding: 0 20upx;

			.icon {
				display: flex;
				flex-direction: column;
				font-size: 28upx;
				width: 90upx;
				justify-content: center;
				align-items: center;

				image {
					height: 40upx;
				}
			}

			.btn {
				flex: 2;
				height: 80upx;
				line-height: 80upx;
				font-size: 28upx;
				color: #fff;
				border-radius: 100upx;
				background-color: #FB852F;
				margin-left: 20upx;
			}
		}

		.pro_info {
			margin-top: 20upx;
			background-color: #fff;
			height: 3000upx;
			width: 100%;

			.pro_tit {
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
