<template>
	<view class="login">
		<image src="@/static/images/login-bg.png" mode="" class="l-bg"></image>
		<view class="form-wrap">
			<u--form 
			labelPosition="left"
			:model="userInfo"
			:rules="rules"
			ref="uForm">
				<u-form-item label="账号:" prop="name" labelWidth="80" :required="true">
					<u-input v-model="userInfo.name" placeholder="请输入您的账户" border="surround"></u-input>
				</u-form-item>
				<u-form-item label="密码:" prop="password" :required="true" labelWidth="80">
					<u-input 
					v-model="userInfo.password" 
					placeholder="请输入您的密码" 
					border="surround" 
					:type="eyeName=='eye-fill'?'text':'password'"
					>
						<template slot="suffix">
							<u-icon @click="showPwd" :name="eyeName" size="24"></u-icon>
						</template>
					</u-input>
				</u-form-item>
				<u-form-item label="验证码:" :required="true" prop="code" labelWidth="80">
					<u-input  v-model="userInfo.code" placeholder="请输入您的验证码" border="surround"></u-input>
					<template slot="right">
						<view  class="code-wrap ml20">
							<view class="code"  v-if="buttonStatus" @click="sendSms">
								获取验证码
							</view>
							<view class="code-text row " v-else>
								<u-count-down 
								:autoStart="false"
								:time="59* 1000" 
								format="ss" 
								@finish="showButton"
								ref="countdown" >
								</u-count-down>
								S后重发
							</view>
						</view>
					</template>
					
				</u-form-item>
			</u--form>
		</view>
		<view class="btn-wrap">
			<view class="btn" @click="submit">
				登录
			</view>
			<view class="other row mt20">
				<view class="o-btn mr30" @click="navTo('/pages/register/register')">注册账号</view>
				<view class="o-btn" @click="navTo('/pages/findPwd/findPwd')">忘记密码</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userInfo:{
					name:'',
					password:'',
					code:''
				},
				eyeName:'eye-off',
				buttonStatus:true,
				rules:{
					name:[{
						type:'string',
						required: true,
						message: '请输入账号',
						trigger: ['blur', 'change']
					}],
					password:[{
						type:'string',
						required: true,
						message: '请输入密码',
						trigger: ['blur', 'change']
					}],
					code:[{
						type:'string',
						required: true,
						message: '请输入验证码',
						trigger: ['blur', 'change']
					}],
				}
			};
		},
		onReady() {
			this.$refs.uForm.setRules(this.rules)
		},
		watch:{
			buttonStatus(val){
				if(!val){
					setTimeout(()=>{
						this.$refs.countdown.start()
					},500)
				}
			},
		},
		methods:{
			showPwd(){
				this.eyeName=this.eyeName=='eye-off'?'eye-fill':'eye-off'
			},
			sendSms(){
				this.showButton()
			},
			showButton() {
				this.buttonStatus = !this.buttonStatus
			},
			submit(){
				console.log(this.$refs.uForm)
				this.$refs.uForm.validate().then(res => {
					console.log(111)
				}).catch(errors => {
					console.log(2222,errors)
				})
			},
		}
	}
</script>

<style lang="scss" scoped>
.login{
	height: 100vh;
	background-color: #fff;
	.l-bg{
		width: 750upx;
		height: 610upx;
	}
	.form-wrap{
		padding: 10upx 45upx;
		.code-wrap{
			width: 156upx;
			height: 70upx;
			text-align: center;
			line-height: 70upx;
			border-width: 2upx ;
			border-color: #dadbde ;
			border-style: solid;
			border-radius: 14upx;
			font-size: 26upx;
			color: #999;
			.code-text{
				/deep/ .u-count-down__text{
					color: #999;
				}
				justify-content: center;
			}
		}
	}
	.btn-wrap{
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		.btn{
			width:520upx;
			height: 80upx;
			border-radius: 40upx;
			color: #fff;
			font-size: 36upx;
			font-weight: bold;
			background: linear-gradient(180deg, #FA842B, #FF896E);
			margin-top:130upx;
			text-align: center;
			line-height: 80upx;
		}
		.other{
			.o-btn{
				color: $base-color;
				font-size: 32upx;
			}
		}
	}
}
</style>
