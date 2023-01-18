<template>
	<view class="with-wrap">
		<navbar  @onRightClick="onRightClick" :mysNavConfig="mysNavConfig">
			<view class="r-btn" slot="right">
				账单
			</view>
		</navbar>
		<view class="info-wrap">
			<view class="info">
				<view class="top row jc-sb">
					<view class="left">充值方式</view>
					<view class="right">
						<view class="f28-c999 b row" @click="$refs.comPay.showPay=true">
							<text class="mr20">	{{payMethod}} </text>
							<u-icon name="arrow-right" color="#333333" size="14"></u-icon>
						</view>
					</view>
				</view>
				<view class="money">
					<view class="">
						充值金额
					</view>
					<view class="input row">
						<u-input
						    placeholder="请输入提现金额"
						    v-model="value"
							border="bottom"
						>
							<text slot="prefix" class="sym">￥</text>
						</u-input>
					</view>
				</view>
			</view>
			<view class="btn btn_default">
				确认
			</view>
		</view>
		
		<com-pay ref="comPay" title="选择支付方式" @selectPay="selectPay"></com-pay>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mysNavConfig:{
					isHome:true,
					navPadding:true,
					navFixed:true,
					bgColor:'#fff',
					navTitle:{
						text: "提现",
					}
				},
				payMethod:'请选择',
				value:''
			};
		},
		methods:{
			onRightClick(){
				
			},
			selectPay(index){
				this.payMethod=index==1?'支付宝':'微信'
			}
		}
	}
</script>

<style lang="scss" scoped>
.with-wrap{
	.r-btn{
		color: #333;
	}
	.info-wrap{
		padding: 24upx 30upx;
		.info{
			background-color: #fff;
			border-radius: 8upx;
			padding: 24upx 30upx 50upx 24upx;
			.top{
				margin-bottom: 22upx;
				padding-bottom: 22upx;
				border-bottom: 2upx solid #F0F0F0;
			}
		}
		.sym{
			color: #333;
			font-size: 65upx;
			font-weight: 600;
		}
	}
	.btn{
		margin-top: 72upx;
	}
}
</style>
