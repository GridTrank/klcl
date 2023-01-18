<template>
	<view>
		<u-popup :show="showPay" @close="showPay=false" round="20">
			<view class="pay-wrap">
				<view class="title">
					{{title}}
				</view>
				<view class="list">
					<view class="item row jc-sb" v-for="(item,index) in payList" :key="index" @click="selectPay(item,index)">
						<view class="left row">
							<image :src="item.path" class="l-img"></image>
							<view class="l-info">
								<view class="l-t1 f32-c333">{{item.label}}</view>
								<view class="l-t2 ">快速支付方便快捷</view>
							</view>
						</view>
						<u-icon v-if="active===index" name="checkmark" color="#FB852F" size="18"></u-icon> 
					</view>
				</view>
			</view>
			
		</u-popup>
	</view>
</template>

<script>
	export default {
		name:"com-pay",
		data() {
			return {
				showPay:false,
				payList:[
					{label:'微信支付',path:require('@/static/images/weixin.png'),value:1},
					{label:'支付宝支付',path:require('@/static/images/zhifub.png'),value:2},
				],
				active:null
			};
		},
		props:{
			title:{
				type:String,
				default:'标题'
			}
		},
		methods:{
			selectPay(item,index){
				this.active=index
				this.showPay=false
				this.$emit('selectPay',index)
			}
		}
	}
</script>

<style lang="scss">
	.pay-wrap{
		padding: 50upx;
		border-radius: 20upx 20upx 0 0;
	}
	.title{
		text-align: center;
	}
	.list{
		margin-top: 80upx;
		.item{
			padding-bottom: 35upx;
			border-bottom: 2upx solid #F3F3F3;
			margin-bottom: 30upx;
			.l-img{
				width: 64upx;
				height: 64upx;
				margin-right: 14upx;
			}
			.l-t2{
				color: #666;
				font-size: 24upx;
				margin-top: 19upx;
			}
		}
	}
</style>