<template>
	<view class="feed-wrap page-fff">
		<view class="tit f32-c333">
			反馈意见
		</view>
		<u--textarea  v-model="content" placeholder="请输入内容" ></u--textarea>
		<view class="mt20 f32-c333">
			联系方式
		</view>
		<u--input
		    placeholder="请输入手机号码(非必填)"
		    border="bottom"
		    v-model="phone"
		></u--input>
		
		<view class="btn">
			提交意见
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content:'',
				phone:''
			};
		}
	}
</script>

<style lang="scss" scoped>
.feed-wrap{
	padding: 30upx;
	.tit{
		margin-bottom: 20upx;
	}
	.btn{
		position: fixed;
		width: 	310upx;
		height: 80upx;
		line-height: 80upx;
		background-color: $base-color;
		color: #fff;
		font-size: 32upx;
		text-align: center;
		border-radius: 8upx;
		bottom: 300upx;
		left: 50%;
		transform: translateX(-50%);
	}
}
</style>
