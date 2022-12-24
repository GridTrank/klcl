<template>
	<view class="order model-wrap mt20">
		<view class="info1 row jc-sb">
			<text class="f32-c333 fwb">山东省某市→陕西省-某市 </text>
			<text class="f22-c999">8-23-12：00</text>
		</view>
		<view class="info2 f28-c333 mt20">
			货车 | 3小时 | B1| 距离：800KM
		</view>
		<view class="info3 mt10">
			价格：9999元
		</view>
		<view class="info4 mt10 f28-c666">
			营运需求:
		</view>
		<view class="info5 mt10 row jc-sb">
			<view class="left row">
				<image src="@/static/images/home-dd.png" mode="" class="l-img mr10"></image>
				<view class="left-info">
					<view class="l-txt f26-c666">姓名</view>
					<view class="l-txt f26-c666">工作日期：2020年12月12日</view>
				</view>
			</view>
			<view class="right" @click="navTo('/pagesB/orderDetail/orderDetail')">
				我要接单
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"orderList",
		data() {
			return {
				
			};
		},
		props:{
			info:{
				type:Object,
				default:()=>{
					return {}
				}
			}
		}
	}
</script>

<style lang="scss">
.order{
	.info3{
		color: #FB8531;
		font-size: 28upx;
		font-weight: bold;
	}
	.info5{
		.left{
			.l-img{
				width: 60upx;
				height: 60upx;
				border-radius: 50%;
			}
		}
		.right{
			width: 173upx;
			height: 58upx;
			background-color: #FB8531;
			color: #fff;
			font-size: 26upx;
			text-align: center;
			line-height: 58upx;
			border-radius: 30upx;
		}
	}
}
</style>