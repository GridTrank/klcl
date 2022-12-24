<template>
	<view class="msg-con">
		<scroll-view scroll-y="true" :style="{'height':screenHeight+'px'}" class="scroll-wrap" :scroll-top="scrollTop">
			<view class="msg-list " id="scroll-box">
				<view :class="['item' ,'mt20', 'row',{'right': item.name==2}]"  v-for="(item,index) in list" :key="index">
					<image src="@/static/images/car1.png" class="u-img"></image>
					<view class="con">
						{{item.content}}
					</view>
				</view>
			</view>
		</scroll-view>
		
		<view class="input-wrap row jc-sb">
			<view class="input-box row jc-sb">
				<view class="inp-box">
					<u--input placeholder="请输入您的信息" border="surround" v-model="content" :adjustPosition="true"></u--input>
				</view>
				<view class="send ml20" @click="send">
					发送
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				screenHeight:'',
				content:'',
				scrollTop:0,
				list:[
					{
						name:1,
						content:'左边左边左边左边左边',
					},
					{
						name:2,
						content:'右边右边右边右边右边',
					},
					{
						name:1,
						content:'左边左边左边左边左边',
					},
					{
						name:1,
						content:'左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边左边',
					},
					{
						name:2,
						content:'右边右边右边右边右边',
					},
					{
						name:2,
						content:'右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边右边',
					}
				]
			};
		},
		onLoad() {
			this.screenHeight=getApp().globalData.sysSize.safeHeight-20
			uni.setNavigationBarTitle({
				title:'张三'
			})
		},
		methods:{
			send(){
				console.log(123,this.content)
				this.list.push({
					name:1,
					content:this.content
				})
				this.scrollToBottom()
			},
			scrollToBottom() {
				let query = uni.createSelectorQuery().in(this);
				setTimeout(res => {
					query.select('#scroll-box').boundingClientRect(data => {
						this.scrollTop = data.height
					}).exec();
				}, 200)
			},
		}
	}
</script>

<style lang="scss" scoped>
	.msg-con{
		position: relative;
		padding-bottom: 200upx;
		
		.msg-list{
			padding: 0 30upx;
			.item{
				.u-img{
					width: 86upx;
					height: 86upx;
					margin-right: 6upx;
					flex-shrink: 0;
				}
				.con{
					padding: 15upx 17upx;
					background-color: #fff;
					border-radius: 8upx;
					color: #333;
					font-size: 32upx;
				}
				&.right{
					flex-direction: row-reverse;
					.con{
						background-color: $base-color;
						color: #fff;
					}
				}
			}
		}
		.input-wrap{
			background-color: #F5F6F8;
			padding: 15upx 30upx ;
			padding-bottom: constant(safe-area-inset-bottom); //兼容 IOS<11.2
			padding-bottom: env(safe-area-inset-bottom);
			box-shadow: 0px 11px 25px 2px #C6C6C6;
			position: fixed;
			bottom: 0%;
			left: 0;
			width: 690upx;
			.input-box{
				padding-bottom: 20upx;
				width: 690upx;
			}
			.inp-box{
				width: 88%;
				background-color: #fff;
			}
			.send{
				background-color: $base-color;
				color: #fff;
				font-size: 32upx;
				width: 100upx;
				height: 70upx;
				text-align: center;
				line-height: 70upx;
				border-radius: 8upx;
			}
		}
	}

</style>
