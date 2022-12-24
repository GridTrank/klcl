<template>
	<view class="update-car">
		<view class="tit f32-c333 b">
			上传信息
		</view>
		<u--form
		labelPosition="left"
		:model="info"
		ref="uForm">
			<u-form-item  prop="name" label="驾驶证名称:" borderBottom labelWidth="100">
				<u-input v-model="info.name" placeholder="请输入您的驾驶证名称" border="none" ></u-input>
			</u-form-item>
			<u-form-item  prop="name" label="准驾车辆:" borderBottom labelWidth="100">
				<u-input v-model="info.name" placeholder="请输入您的准驾车辆" border="none" ></u-input>
			</u-form-item>
			<u-form-item  prop="name"  borderBottom >
				<view class="upload">
					<view class="u-t">上传照片:</view>
					<u-upload
						class="mt20"
						:fileList="fileList"
						@delete="deletePic"
						@afterRead="afterRead"
						name="4"
						multiple
						:maxCount="2"
					></u-upload>
				</view>
			</u-form-item>
		</u--form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				info:{},
				fileList:[
					{
						url: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
					},
					{
						url: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
					}
				]
			};
		},
		methods:{
			afterRead(e){
				console.log(123,e)
				
			},
			deletePic(event) {
				this.fileList.splice(event.index, 1)
			},
		}
		
	}
</script>

<style lang="scss" scoped>
.update-car{
	background-color: #fff;
	min-height: 100vh;
	padding-top: 45upx;
	.tit{
		margin-left:38upx ;
	}
	.upload{
		.u-t{
			font-size: 30upx;
			color: #333;
		}
	}
	/deep/ .u-form-item__body{
		padding: 20upx 38upx;
	}
}
</style>
