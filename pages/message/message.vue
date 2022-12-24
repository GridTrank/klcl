<template>
	<view class="msg-wrap">
		<view class="msg-list">
			<view class="msg-item mt20 row jc-sb" v-for="(item,index) in 16" :key="index" @click="navTo('./msgDetail')">
				<view class="left row">
					<image src="@/static/images/storyboard.png" class="l-img mr10"></image>
					<view class="column info jc-sb">
						<text class="f28-c333">系统通知</text>
						<text class="f26-c666 mt20">内容</text>
					</view>
				</view>
				<view class="right">
					<view class="column info jc-sb">
						<text class="f24-c999">16:24</text>
						<text class="num mt20">1</text>
					</view>
				</view>
			</view>
		</view>
		
		<tabbar :activeIndexProp="1"></tabbar>
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
	.msg-wrap{
		padding-bottom: 200upx;
		.msg-list{
			padding: 23upx 30upx;
			.msg-item{
				background-color: #FFFFFF;
				border-radius: 8upx;
				padding: 12upx;
				height: 100upx;
				.left{
					.l-img{
						width: 85upx;
						height: 85upx;
						border-radius: 50%;
					}
					.info{
						align-items: baseline;
					}
				}
				.right{
					.info{
						align-items: flex-end;
						.num{
							width: 25upx;
							height: 25upx;
							text-align: center;
							line-height: 25upx;
							font-size: 20upx;
							color: #fff;
							background-color: $base-color;
							border-radius: 50%;
						}
					}
					
				}
				
				
			}
		}
	}

</style>
