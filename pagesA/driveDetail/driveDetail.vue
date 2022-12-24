<template>
	<view class="drive-wrap">
		<navbar  :mysNavConfig="mysNavConfig"  >
			<view class="search-left" slot="left" @click="navTo('back')">
				<i class="iconfont">&#xe630;</i>
			</view>
			<view class="search-left" slot="center1">
				司机详情
			</view>
		</navbar>
		<image src="@/static/images/sj-bg.png" mode="" class="drive-bg"></image>
		<view class="card top">
			<view class="f32-c333">张某某</view>
			<view class="f26-c666 mt10">
				驾龄：5年 | A1驾驶证
			</view>
			<view class="f26-c666 mt10">
				已服务50次
			</view>
			<image src="@/static/images/car2.png" mode="" class="d-img"></image>
		</view>
		<view class="card mt10">
			<view class="row">
				<text class="f32-c333">准驾车型：</text>
				<text class="f28-c666"> 手动挡汽车、自动挡汽车、低速载货汽车</text>
			</view>
			<view class="row mt20">
				<text class="f32-c333">服务指数：</text>
				<u-rate :count="5" :value="3.5" :allowHalf="true" :readonly="true" activeColor="#FB852F" inactiveColor="#FB852F"></u-rate>
				<text class="rate">3.5分</text>
			</view>
		</view>
		<view class="card mt10">
			<view class="f32-c333">
				简介：
			</view>
			<view class="f28-c333 mt10">
				司机简介司机简介司机简介司机简介司机 撒旦司
				简介司机  司机简介司机简介司机简介司机简介简介司司
				司机简介司机简介司机简介司机简介司机简介司啊范德
				机简介司机简介司机简介司机简介司机简介司机简介司
				简介司机简介司机简介司机简介司机简介司机简简介司
				介司机简介司机简介
			</view>
			<view class="btn-wrap row">
				<view class="left btn">
					收藏
				</view>
				<view class="right btn">
					联系师傅
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mysNavConfig:{
					navFixed:true,
					bgColor:'transparent',
				},
			};
		}
	}
</script>

<style lang="scss" scoped>
.search-left{
	color: #fff;
}
.drive-bg{
	width:100%;
	height: 253upx;
	position: fixed;
	top: 0;
	left: 0;
	z-index: 1;
}
.card{
	background-color: #fff;
	padding: 17upx 30upx;
	&.top{
		margin-top: 253upx;
		position: relative;
		.d-img{
			width: 190upx;
			height: 190upx;
			position: absolute;
			z-index: 11;
			top: -80upx;
			right: 30upx;
		}
	}
	.rate{
		color: $base-color;
		font-size: 26upx;
	}
	.btn-wrap{
		justify-content: flex-end;
		margin-top: 50upx;
		.btn{
			width: 200upx;
			height: 68upx;
			line-height: 68upx;
			text-align: center;
			border-radius: 34upx;
			color: #fff;
			font-size: 32upx;
			margin-left: 37upx;
			background-color: $base-color;
		}
	}
}
</style>
