<template>
	<view class="car-type">
		<view class="model-wrap">
			<view class="f32-c333">常用汽车</view>
			<view class="list row ">
				<view class="item column" v-for="(item,index) in 7" :key="index">
					<image src="@/static/images/car2.png" mode="" class="c-img"></image>
					<text class="f26-c333 mt10">汽车名称</text>
				</view>
			</view>
		</view>
		<view class="model-wrap mt20">
			<view class="f32-c333">特殊车型</view>
			<view class="list row ">
				<view class="item column" v-for="(item,index) in 8" :key="index">
					<image src="@/static/images/car2.png" mode="" class="c-img"></image>
					<text class="f26-c333 mt10">汽车名称</text>
				</view>
			</view>
		</view>
		<view class="model-wrap mt20">
			<view class="f32-c333">特殊车型</view>
			<image @click="navTo('/pagesA/updateCar/updateCar')" src="@/static/images/jia1.png" mode="" class="c-img mt10"></image>
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
.car-type{
	padding: 30upx;
	.model-wrap{
		padding: 20upx;
	}
	.list{
		flex-wrap: wrap;
		.item{
			margin-right:48upx;
			&:nth-child(4n){
				margin-right: 0;
			}
		}
	}
	
	.c-img{
		width: 125upx;
		height: 125upx;
	}
}
</style>
