<template>
	<view class="tab-bar">
		<view class="tab-list row jc-sa">
			<view class="tab-item column" :class="'tab'+index" v-for="(item,index) in list" :key="index" @click="tabHandle(item,index)">
				<template v-if="index!==2">
					<image :src="activeIndexProp===index?item.selectIcon:item.icon" class="t-img"></image>
					<view :class="['t-txt',{'active':activeIndexProp===index}]">{{item.label}}</view>
				</template>
				<template v-else>
					<view class="item3 row">
						<view class="btn left" @click.stop="orderHandle(1)">
							<text>订单发布</text>
						</view>
						<view class="btn right" @click.stop="orderHandle(2)">
							<text>司机入驻</text>
						</view>
					</view>
				</template>
			</view>
		</view>
		<u-popup :show="showAdd" @close="closePopup" >
		    <view>
		        <text>出淤泥而不染，濯清涟而不妖</text>
		    </view>
		</u-popup>
	</view>
</template>

<script>
	export default {
		name:"tabbar",
		data() {
			return {
				value6:0,
				activeIndex:0,
				showAdd:false,
				list:[
					{
						label:'首页',
						path:'/pages/home/home',
						icon:require('@/static/tabbar/home.png'),
						selectIcon:require('@/static/tabbar/home-a.png')
					},
					{
						label:'消息通知',
						path:'/pages/message/message',
						icon:require('@/static/tabbar/msg.png'),
						selectIcon:require('@/static/tabbar/msg-a.png')
					},
					{},
					{
						label:'接单大厅',
						path:'/pages/order/order',
						icon:require('@/static/tabbar/order.png'),
						selectIcon:require('@/static/tabbar/order-a.png')
					},
					{
						label:'我的',
						path:'/pages/user/user',
						icon:require('@/static/tabbar/user.png'),
						selectIcon:require('@/static/tabbar/user-a.png')
					}
				]
			};
		},
		props:{
			activeIndexProp:{
				default:0
			}
		},
		methods:{
			tabHandle(item,index){
				if(index==2)return
				uni.switchTab({
					url:item.path
				})
			},
			orderHandle(e){
				if(e===1){
					this.navTo('/pagesB/releaseOrder/releaseOrder')
				}else{
					this.navTo('/pagesB/driverEnter/driverEnter')
				}
			},
			changeTabbar(e){
				if(e===2){
					this.showAdd=true
					return
				}
			},
			closePopup(e){
				this.showAdd=false
			}
		}
	}
</script>

<style lang="scss">
	.tab-bar{
		position: fixed;
		bottom: 0;
		padding-bottom: constant(safe-area-inset-bottom); //兼容 IOS<11.2
		padding-bottom: env(safe-area-inset-bottom);
		width: 100%;
		background-color: #fff;
		box-shadow: 0px 11px 25px 2px #C6C6C6;
		.tab-list{
			padding: 20upx;
			.tab-item{
				&.tab2{
					width: 30%;
				}
				.t-img{
					width: 40upx;
					height: 40upx;
				}
				.t-txt{
					font-size: 24upx;
					&.active{
						color: #FA842B;
					}
				}
				.item3{
					position: absolute;
					width: 240upx;
					border-radius: 70px 70px 0 0;
					background-color: #fff;
					top: -30upx;
					padding: 10upx 10upx 0 10upx;
					.btn{
						border-radius: 70px 0 0 0;
						width: 120upx;
						height: 120upx;
						background-color: #FCCD4D;
						color: #fff;
						font-size: 26upx;
						display: flex;
						align-items: center;
						justify-content: center;
						text{
							display: inline-block;
							width: 35px;
							height: 35px;
							text-align: center;
							margin-top: 30upx;
							padding: 15upx;
						}
						&.left{
							justify-content: flex-end;
						}
						&.right{
							border-radius: 0  70px 0 0;
							justify-content: flex-start;
							background-color: #FA842B;
						}
					}
				}
			}
		}
	}
.add{
	width: 80upx;
	height: 80upx;
}
</style>