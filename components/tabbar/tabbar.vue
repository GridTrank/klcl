<template>
	<view class="tab-bar">
		<view class="tab-list row jc-sa">
			<view class="tab-item column" :class="'tab'+index" v-for="(item,index) in list" :key="index" @click="tabHandle(item,index)">
				<image :src="activeIndexProp===index?item.selectIcon:item.icon" class="t-img"></image>
				<view :class="['t-txt',{'active':activeIndexProp===index}]">{{item.label}}</view>
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
					// {
					// 	label:'客服',
					// 	path:'/pages/message/message',
					// 	icon:require('@/static/tabbar/msg.png'),
					// 	selectIcon:require('@/static/tabbar/msg-a.png')
					// },
					// {
					// 	label:'直播',
					// 	path:'/pages/message/message',
					// 	icon:require('@/static/tabbar/msg.png'),
					// 	selectIcon:require('@/static/tabbar/msg-a.png')
					// },
					{
						label:'分享',
						path:'/pages/share/share',
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
		onLoad() {
			uni.hideTabBar()
		},
		methods:{
			tabHandle(item,index){
				if(index){
					if(this.$util.isLogin()){
						uni.switchTab({
							url:item.path
						})
					}
					
				}else{
					uni.switchTab({
						url:item.path
					})
				}
			
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
			}
		}
	}
.add{
	width: 80upx;
	height: 80upx;
}
</style>