<template>
	<view class="ex-wrap">
		<view class="top row jc-sb">
			<image src="@/static/images/gth.png" mode="widthFix" class="g-img"></image>
			<view class="txt">
				您的入驻请求已通过! 请您缴纳保证金并签署合同!
			</view>
			<u-icon name="close" color="#fff" size="12"></u-icon>
		</view>
		<view class="info">
			<view class="i-tit f28-c333">保证金金额</view>
			<view class="i-m b">￥{{9999}}</view>
		</view>
		<view class="bo">
			点击此处查看并签署合同
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss" scoped>
.ex-wrap{
	background-color: #fff;
	min-height: 100vh;
	.top{
		background-color: $base-color;
		height: 83upx;
		padding: 0 32upx;
		.g-img{
			width: 30upx;
			height: 30upx;
		}
		.txt{
			font-size: 28upx;
			color: #fff;
		}
	}
	.info{
		padding: 50upx 32upx;
		.i-m{
			color: #333;
			font-size: 65upx;
		}
	}
	.bo{
		border-top: 2upx solid #f2f2f2;
		padding: 20upx 32upx;
		color: #E12D25;
		font-size: 26upx;
	}
}
</style>
