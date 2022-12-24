<template>
	<view class="start" >
		<image class="s-img" src="@/static/images/storyboard.png" mode=""></image>
		<view class="btn" @click="navTo('/pages/home/home','switch')">
			立即进入
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		onLoad() {
			setTimeout(()=>{
				this.navTo('/pages/home/home','switch')
			},5000)
		}
	}
</script>

<style lang="scss" scoped>
.s-img{
	width: 750upx;
	height: 100vh;
	position: fixed;
	top: 0;
	left: 0;
}
.btn{
	width: 425upx;
	height: 98upx;
	border-radius: 22upx;
	background-color: #fff;
	text-align: center;
	line-height: 98upx;
	color: $base-color;
	font-size: 54upx;
	position: absolute;
	bottom: 200upx;
	left: 50%;
	transform: translateX(-50%);
}
</style>
