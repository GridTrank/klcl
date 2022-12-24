<template>
	<view class="contact-wrap">
		<view class="model">
			<image src="@/static/images/lxwm.png" mode="widthFix" class="l-img"></image>
			<view class="f32-c333 b mt20">欢迎您来电话咨询</view>
		</view>
		<view class="model bo ">
			<view class="m-card">
				<view class="m1">公司电话</view>
				<view class="m2">182****1234</view>
			</view>
			<view class="m-card mt30">
				<view class="m1">公司邮箱</view>
				<view class="m2">182****1234</view>
			</view>
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
.contact-wrap{
	background-color: #fff;
	min-height: 100vh;
	.model{
		padding: 30upx;
		.l-img{
			width: 100%;
			height: 180upx;
		}
		&.bo{
			border-top: 2upx solid #f2f2f2;
		}
		.m2{
			color: $base-color;
			font-size: 30upx;
		}
	}
	
}
</style>
