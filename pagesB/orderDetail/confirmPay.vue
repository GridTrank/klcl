<template>
	<view class="confirm-wrap">
		<view class="item row">
			<text class="f28-c333 left">订单编号：</text>
			<text class="f28-c333 b">测试</text>
		</view>
		<view class="item row">
			<text class="f28-c333 left">支付方式：</text>
			<view class="f28-c333 b row" @click="$refs.comPay.showPay=true">{{payMethod}} <u-icon name="arrow-right" color="#333333" size="14"></u-icon></view>
		</view>
		<view class="item row">
			<text class="f28-c333 left">支付金额：</text>
			<text class="f28-c333 b">测试</text>
		</view>
		<view class="item  row">
			<text class="f28-c333 left">订单时间：</text>
			<text class="f28-c333 b">测试</text>
		</view>
		<view class="item row">
			<text class="f28-c333 left">订单金额：</text>
			<text class="f28-c333 b">测试</text>
		</view>
		<view class="item row">
			<text class="f28-c333 left">实付金额：</text>
			<text class="f28-c333 b">测试</text>
		</view>
		<view class="item row">
			<text class="f28-c333 left">支付倒计时：</text>
			<text class="f28-c333 b">测试</text>
		</view>
		
		<view class="btn-wrap ">
			<view class="btn" @click="toPay">
				确认支付
			</view>
		</view>
		<com-pay ref="comPay" title="选择支付方式" @selectPay="selectPay"></com-pay>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				info:{},
				payMethod:'请选择'
			};
		},
		methods:{
			toPay(){
				uni.navigateTo({
					url:'./confirmPay'
				})
			},
			selectPay(index){
				this.payMethod=index==1?'支付宝':'微信'
			}
		}
	}
</script>

<style lang="scss" scoped>
.confirm-wrap{
	.item{
		background-color: #fff;
		border-bottom: 2upx solid #f2f2f2;
		padding: 20upx 30upx;
		justify-content: space-between;
		.left{
			// width: 150upx;
		}
	}
	.content{
		padding: 30upx;
		.title{
			font-size: 32upx;
			color: $base-color;
			font-weight: bold;
			margin-bottom: 10upx;
		}
	}
	.btn-wrap{
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top:300upx;
		.btn{
			width: 430upx;
			height: 84upx;
			border-radius: 8upx;
			background-color: $base-color;
			color: #fff;
			font-size:40upx;
			text-align: center;
			line-height: 84upx;
		}
	}
}
</style>
