<template>
	<view class="product_info">
		<image src="@/static/home1.png" class="c-img"></image>
		<view class="info column jc-sb">
			<view class="name twoHidden">名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称名称</view>
			<view class="price">
				<text class="p1"> ￥123 </text>
				<text class="p2"> ￥123 </text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"productInfo",
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss" scoped>
.product_info{
	width: 100%;
	height: auto;
	flex-shrink: 0;
	background-color: #fff;
	border-radius: 20upx;
	overflow: hidden;
	.c-img{
		height: 200upx;
		width: 100%;
		display: block;
	}
	.info{
		height: 160upx;
		background-color: #fff;
		padding: 20upx;
		align-items: flex-start;
		.price{
			.p1{
				color: $base-color;
				font-size: 36upx;
				font-weight: 600;
				margin-right: 8upx;
			}
			.p2{
				color: #999;
				text-decoration: line-through;
			}
		}
	}
}
</style>