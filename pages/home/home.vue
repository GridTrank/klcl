<template>
	<view class="home-wrap">
		<view class="index-top">
			<view class="nav-wrap">
				<view class="s-wrap row" @click="toSearch">
					<image src="@/static/images/search.png" class="icon-img"></image>
					<text>请输入</text>
				</view>
				<view class="search" slot="right">
					搜索
				</view>
			</view>
			<view class="index-bg">
				<u-swiper :list="list1" circular indicator :autoplay="true" height="150">
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

				<block v-for="(item,index) in menuList" :key="index">
					<view class="cate-item column" v-if="menuList.length > 8 && index == limiMenu"
						@click="limiMenu = 99">
						<image src="@/static/more.jpg" class="c-img more"></image>
						<text class="c-label">查看更多</text>
					</view>
					<view class="cate-item column" v-else-if="index < limiMenu+1" @click="toCate(item)">
						<image :src="item.imgPreviewUrl" class="c-img"></image>
						<text class="c-label">{{item.name}}</text>
					</view>
				</block>
			</view>
			<view class="cate-swiper">
				<u-swiper @click="toDetail" :list="newSwiper.map(item=>item.imageBase64)" circular indicator :autoplay="true" height="150">
				</u-swiper>
			</view>

		</view>
		<view class="buying-wrap">
			<view class="title">
				限时抢购
			</view>
			<scroll-view class="mt20" scroll-x="true">
				<view class="buying-list">
					<view class="buying-item" v-for="(item,index) in timeLimitList" :key="index">
						<image src="@/static/home1.png" class="b-img"></image>
						<view class="name twoHidden">{{item.title}}</view>
						<view class="buy_info">
							<view class="price-wrap">
								<text class="p1">￥{{item.rushPurchasePrice}}</text>
								<text class="p2">￥{{item.price}}</text>
							</view>
							<view class="time">
								{{item.limitedEndTime}}
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
		
	
		<view class="con-box" style="background-color: #A8CACE;">
			<view class="con-top row jc-sb">
				<view class="title">
					近期上新 New Arrival
				</view>
				<view class="more" @click="toCate({id:'new'})">
					查看更多
				</view>
			</view>
			<!-- <image :src="home0" class="con-image" mode="widthFix"></image> -->
			<view class="list ">
				<view class="item" v-for="(item,index) in newList" :key="index">
					<productInfo :info="item" type="row"></productInfo>
				</view>

			</view>
		</view>

		<view class="con-box" style="background-color: #EA8D76;">
			<view class="con-top row jc-sb">
				<view class="title">
					餐饮美食 Dining Gourmet Food
				</view>
				<view class="more" @click="toCate({id:'aefea9af872c4788b60a1a37f9774bee'})">
					查看更多
				</view>
			</view>
			<image :src="home0" class="con-image" mode="widthFix"></image>
			<view class="list">
				<view class="item" v-for="(item,index) in productList0" :key="index">
					<productInfo :info="item"></productInfo>
				</view>

			</view>
		</view>

		<view class="con-box box2" style="background-color: #B34422;">
			<view class="con-top row jc-sb">
				<view class="title">
					休闲娱乐 Leisure Entertainment
				</view>
				<view class="more" @click="toCate({id:'031f595f174c486888a11523528a91c4'})">
					查看更多
				</view>
			</view>
			<image :src="home1" class="con-image" mode="widthFix"></image>
			<view class="list ">
				<view class="item" v-for="(item,index) in productList1" :key="index">
					<productInfo :info="item"></productInfo>
				</view>
			</view>
		</view>

		<view class="con-box box2" style="background-color: #47CF97 ;">
			<view class="con-top row jc-sb">
				<view class="title">
					研学旅游 Study Tourism
				</view>
				<view class="more" @click="toCate({id:'8f665bc4e69d40d78883c12c3e24ca4f'})">
					查看更多
				</view>
			</view>
			<image :src="home2" class="con-image" mode="widthFix"></image>
			<view class="list">
				<view class="item" v-for="(item,index) in productList2" :key="index">
					<productInfo :info="item"></productInfo>
				</view>
			</view>
		</view>

		<view class="con-box box2" style="background-color:#E2B07B ;">
			<view class="con-top row jc-sb">
				<view class="title">
					找好工作 Find  Good Job
				</view>
				<view class="more" @click="toCate({id:'58cfe42dbbc14acb9c85a5e5a76365f9'})">
					查看更多
				</view>
			</view>
			<image :src="home3" class="con-image" mode="widthFix"></image>
			<view class="list">
				<view class="item" v-for="(item,index) in productList3" :key="index">
					<productInfo :info="item"></productInfo>
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
				home0: '',
				home1: '',
				home2: '',
				home3: '',

				productList0: [],
				productList1: [],
				productList2: [],
				productList3: [],
				menuList: [],
				timeLimitList: [],
				newList:[],
				newSwiper:[],
				limiMenu: 7,
				mysNavConfig: {
					isHome: false,
					navPadding: false,
					navFixed: false,
					// searchConfig:{
					// 	placeholder:'输入关键词搜索'
					// }
				},
				list1: [
					require('@/static/home1.png'),
					require('@/static/home1.png'),
					require('@/static/home1.png'),
				],
				cateList: [

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
			this.init()
		},
		onPullDownRefresh(res) {
			setTimeout(() => {
				uni.stopPullDownRefresh()
			}, 3000)
		},
		methods: {
			init() {
				this.$http(`/my-system/wechatMenu/list`, {
					size: 99
				}, 'post').then(res => {
					this.menuList = res.rows

				})
				this.$http(`/my-merchandise/timeLimitCommodity/list`, {
					size: 99
				}, 'post').then(res => {
					this.timeLimitList = res.rows;
				})
				this.$http(`/my-merchandise/commodity/newList`, {
					size: 10
				}, 'post').then(res => {
					this.newList = res.rows;
				})
				this.$http(`/my-merchandise/homeRecommend/list`, {
					size: 99
				}, 'post').then(res => {
					this.newSwiper = res.rows
				
				})
				uni.request({
					url: "https://www.my-klcl.cn/api/my-file/file/base64/da7b82e85797392d1e0f16104f51c1c5",
					method: 'GET',
					success: (res) => {
						this.home0 = res.data
					}
				})
				this.$http(`/my-merchandise/commodity/list`, {
					page: 1,
					size: 10,
					wxMenuId: 'aefea9af872c4788b60a1a37f9774bee'
				}, 'post').then(product => {
					this.productList0 = product.rows
				})
				uni.request({
					url: "https://www.my-klcl.cn/api/my-file/file/base64/dae69d23851cc1318723de754d4e94eb",
					method: 'GET',
					success: (res) => {
						this.home1 = res.data
					}
				})
				this.$http(`/my-merchandise/commodity/list`, {
					page: 1,
					size: 10,
					wxMenuId: '031f595f174c486888a11523528a91c4'
				}, 'post').then(product => {
					this.productList1 = product.rows
				})
				uni.request({
					url: "https://www.my-klcl.cn/api/my-file/file/base64/f2dcf80bda14622da81ebf78e388f218",
					method: 'GET',
					success: (res) => {
						this.home2 = res.data
					}
				})
				this.$http(`/my-merchandise/commodity/list`, {
					page: 1,
					size: 10,
					wxMenuId: '8f665bc4e69d40d78883c12c3e24ca4f'
				}, 'post').then(product => {
					this.productList2 = product.rows
				})
				uni.request({
					url: "https://www.my-klcl.cn/api/my-file/file/base64/def6ffd2c07233c5514af0cba3259603",
					method: 'GET',
					success: (res) => {
						this.home3 = res.data
					}
				})
				this.$http(`/my-merchandise/commodity/list`, {
					page: 1,
					size: 10,
					wxMenuId: '58cfe42dbbc14acb9c85a5e5a76365f9'
				}, 'post').then(product => {
					this.productList3 = product.rows
				})
			},
			toDetail(index) {
				uni.navigateTo({
					url: `/pagesA/detail/detail?id=${this.newSwiper[index].commodityId}`
				})
			},
			toCate(item) {
				uni.navigateTo({
					url: `/pagesA/cate/cate?id=${item.id}`,

				})
			},
			toSearch() {
				uni.navigateTo({
					url: '/pagesA/search/search'
				})
			},
			onRightClick() {
				this.toSearch()
				console.log('search')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.home-wrap {
		min-height: 100vh;
		background-color: #fff;
		padding-bottom: 130upx;
	}

	.index-top {
		width: 100%;
		height: 530upx;
		background-color: #DBD9B7;
		background-image: url('@/static/bg2.png');
		// padding-bottom: 50upx;
		// padding-top: 100upx;
		.nav-wrap {
			padding: 20upx;
			display: flex;
		}

		.search {
			color: #fff;
			
		}

		.s-wrap {
			padding: 16upx 24upx;
			border-radius: 32upx;
			font-size: 24upx;
			background-color: #fff;
			flex:2;
			.icon-img {
				width: 28upx;
				height: 28upx;
				margin-right: 34upx;
			}
		}

		.index-bg {
			padding: 20upx;
		}

		.top_label {
			padding: 0 20upx;

			.label {
				color: #fff;
			}
		}
	}

	.cate-wrap {
		padding: 30upx;
		background-color: #fff;
		border-radius: 30upx;
		margin-top: -30upx;

		.cate-list {
			flex-wrap: wrap;
			justify-content: space-between;
		}

		.cate-item {
			margin-bottom: 20upx;

			.c-img {
				width: 150upx;
				height: 150upx;
			}

			.more {
				padding: 30upx;
				box-sizing: border-box;
			}
		}

		.cate-swiper {}

	}

	.buying-wrap {
		padding: 30upx;
		// background-image: url('@/static/bg2.png');
		background-color: #F0B2A8;
		border-radius: 30upx;

		.title {
			color: #fff;
			font-size: 40upx;
			font-weight: 600;
			padding-left: 20upx;
			position: relative;

			&::after {
				display: block;
				content: "";
				position: absolute;
				width: 10upx;
				height: 100%;
				background-color: #fff;
				left: 0;
				top: 0;
			}
		}

		.buying-list {
			display: flex;
			flex-wrap: nowrap;
			width: 100%;

			.buying-item {
				width: 260upx;
				display: inline-block;
				margin-right: 20upx;
				background-color: #fff;
				border-radius: 20upx;
				overflow: hidden;
				flex-shrink: 0;

				&:last-child {
					margin-right: 0;
				}

				.b-img {
					width: 260upx;
					height: 260upx;
				}

				.buy_info {
					padding: 20upx;
				}
			}
		}

	}

	.pd20 {
		padding: 20upx;
	}

	.con-box {
		border-radius: 30upx;
		padding: 30upx 20upx;
		margin-top: 30upx;

		.con-image {
			width: 100%;
		}

		.list {
			margin-top: 30upx;

			.item {
				margin-bottom: 20upx;
				border-radius: 20upx;
				overflow: hidden;
				height: 200upx;

			}
		}

		&.box2 {
			.list {
				display: flex;
				align-items: center;
				justify-content: space-between;
				flex-wrap: wrap;

				.item {
					width: 48%;
					height: auto;
					flex-shrink: 0;

					.c-img {
						height: 200upx;
						width: 100%;
						display: block;
					}
				}
			}
		}
	}
</style>
