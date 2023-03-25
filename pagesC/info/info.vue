<template>
	<view class="info-wrap">
		<view class="form-wrap">
			<u--form
			labelPosition="left"
			:model="userInfo"
			ref="uForm">
				<u-form-item  prop="name" label="头像:" borderBottom  labelWidth="100">
					<u-upload
						:fileList="fileList"
						name="1"
						multiple
						:maxCount="1"
					></u-upload>
				</u-form-item>
				<u-form-item  prop="name" label="性别:" borderBottom  labelWidth="100">
					<u-radio-group v-model="userInfo.sex">
						<u-radio shape="circle" label="男" :name="1"></u-radio>
						<u-radio shape="circle" label="女" :name="2"></u-radio>
					</u-radio-group>
				</u-form-item>
				<u-form-item  prop="name" label="年龄:" borderBottom  labelWidth="100">
					<u-input v-model="userInfo.name" placeholder="请输入上岗证类型" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="联系方式:" borderBottom labelWidth="100">
					<u-input v-model="userInfo.name" placeholder="请输入司机费用" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="驾龄:" borderBottom labelWidth="100">
					<u-input v-model="userInfo.name" placeholder="请输入追加费用" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="驾照类型:" borderBottom labelWidth="100">
					<u-input v-model="userInfo.name" placeholder="请输入联系电话" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="上岗证类型:" borderBottom labelWidth="100">
					<u-input v-model="userInfo.name" placeholder="请输入联系电话" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="公司名称:" borderBottom labelWidth="100">
					<u-input v-model="userInfo.name" placeholder="请输入联系电话" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="公司介绍:" borderBottom labelWidth="100">
					<u--textarea v-model="userInfo.name" placeholder="请输入联系电话" border="none" ></u--textarea>
				</u-form-item>
			</u--form>
			<view class="btn-wrap row jc-sb">
				<view class="btn">
					修改
				</view>
				<view class="btn">
					保存
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userInfo:{
					sex:1
				},
				fileList:[]
			};
		}
	}
</script>

<style lang="scss" scoped>
.info-wrap{
	min-height: 100vh;
	background-color: #fff;
	padding: 32upx;
	.btn-wrap{
		width: 60%;
		margin: 0 auto;
		margin-top: 80upx;
	}
}
</style>
