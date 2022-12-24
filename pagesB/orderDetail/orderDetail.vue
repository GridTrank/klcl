<template>
	<view class="release-wrap">
		<view class="form-wrap">
			<u--form
			labelPosition="left"
			:model="orderInfo"
			ref="uForm">
				<u-form-item  prop="name" label="姓名:" borderBottom :required="true" labelWidth="100">
					<u-input v-model="orderInfo.name" placeholder="请输入发布者姓名" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="公司名称:" borderBottom :required="true" labelWidth="100">
					<u-input v-model="orderInfo.name" placeholder="请输入公司名称" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="age" label="驾龄选择:" borderBottom :required="true" labelWidth="100">
					<view @click="optionHandle('ageName')"  class="inp-view">{{ageName}}</view>
					<u-icon
						@click="optionHandle('ageName')" 
						slot="right"
						name="arrow-right"
					></u-icon>
				</u-form-item>
				<u-form-item  prop="level" label="所需驾照:" borderBottom :required="true" labelWidth="100">
					<view @click="optionHandle('levelName')" class="inp-view">{{levelName}}</view>
					<u-icon
						@click="optionHandle('levelName')" 	
						slot="right"
						name="arrow-right"
					></u-icon>
				</u-form-item>
				<u-form-item  prop="name" label="上岗证类型:" borderBottom :required="true" labelWidth="100">
					<u-input v-model="orderInfo.name" placeholder="请输入上岗证类型" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="司机费用:" borderBottom :required="true" labelWidth="100">
					<u-input v-model="orderInfo.name" placeholder="请输入司机费用" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="追加费用:" borderBottom :required="true" labelWidth="100">
					<u-input v-model="orderInfo.name" placeholder="请输入追加费用" border="none" ></u-input>
				</u-form-item>
				<u-form-item  prop="name" label="联系电话:" borderBottom :required="true" labelWidth="100">
					<u-input v-model="orderInfo.name" placeholder="请输入联系电话" border="none" ></u-input>
				</u-form-item>
				
				<u-form-item v-if="type==1" prop="name" label="起始地:" borderBottom :required="true" labelWidth="100">
					<view @click="chooseAddress('start')" class="inp-view row">
						{{startAddress}}
						<u-icon name="map-fill" color="#FB852F" size="20"></u-icon>
					</view>
					<u-icon
						slot="right"
						name="arrow-right"
					></u-icon>
				</u-form-item>
				<u-form-item v-if="type==1"  prop="name" label="目的地:" borderBottom :required="true" labelWidth="100">
					<view @click="chooseAddress('dest')" class="inp-view row">
						{{destAddress}}
						<u-icon name="map-fill" color="#FB852F" size="20"></u-icon>
					</view>
					<u-icon
						slot="right"
						name="arrow-right"
					></u-icon>
				</u-form-item>
				<u-form-item  v-if="type==1" prop="level" label="是否需要返程:" borderBottom :required="true" labelWidth="100">
					<view @click="optionHandle('back')" class="inp-view">{{back}}</view>
					<u-icon
						@click="optionHandle('back')" 	
						slot="right"
						name="arrow-right"
					></u-icon>
				</u-form-item>
				
				<u-form-item v-if="type==2"  prop="name" label="工作地点:" borderBottom :required="true" labelWidth="100">
					<view @click="chooseAddress('start')" class="inp-view row">
						{{startAddress}}
						<u-icon name="map-fill" color="#FB852F" size="20"></u-icon>
					</view>
					<u-icon
						slot="right"
						name="arrow-right"
					></u-icon>
				</u-form-item>
				<u-form-item v-if="type==2"  prop="name" label="工作时长:" borderBottom :required="true" labelWidth="100">
					<u-input v-model="orderInfo.longTime" placeholder="请输入工作时长" border="none" ></u-input>
					
				</u-form-item>
			</u--form>
		</view>
		<view class="map-wrap" v-if="type==1">
			<view class="map-box" v-if="startAddressInfo">
				<view class="title f24-c3332 b">起始地导航</view>
				<com-map ref="comMap" :info="startAddressObj" posiType="start"></com-map>
			</view>
			
			<view class="map-box mt30" v-if="destAddressInfo">
				<view class="title dest f24-c3332 b">目的地地导航</view>
				<com-map :info="destAddressObj" posiType="dest"></com-map>
			</view>
		</view>
		<view class="task-wrap" v-if="type==2 && startAddressInfo">
			<view class="f32-c333 row tit">
				<image src="@/static/images/order-icon3.png" class="o-img mr10"></image>
				地点定位
			</view>
			<com-map  :info="startAddressObj" posiType='start' :type="type"></com-map>
		</view>
		<view class="task-wrap ">
			<view class="f32-c333 row tit">
				<image src="@/static/images/order-icon2.png" class="o-img mr10"></image>
				任务要求
			</view>
			<u--textarea  v-model="content" placeholder="请输入任务要求" ></u--textarea>
		</view>
		<view class="task-wrap ">
			<view class="f32-c333 row tit">
				<image src="@/static/images/order-icon1.png" class="o-img mr10"></image>
				车辆照片
			</view>
			
		</view>
		<view class="btn-wrap mt20">
			<view class="btn" @click="navTo('./confirmOrder')">
				提交订单
			</view>
		</view>
		
		<u-action-sheet
			:show="showOption"
			:actions="options"
			:title="optionsTitle"
			@close="showOption = false"
			@select="selectOption"
		>
		</u-action-sheet>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				type:'',   //1-营运需求，2-代工需求
				orderInfo:{
					age:1
				},
				showOption:false,
				optionsTitle:'',
				ageName:'半年',
				levelName:'A1',
				back:'是',
				optionType:'',
				options:[
					{name:'半年'},
					{name:'1年'},
					{name:'2年'},
					{name:'3年'},
				],
				startAddress:'请选择地址',
				startAddressInfo:'',
				startAddressObj:{},
				destAddress:'请选择地址',
				destAddressInfo:'',
				destAddressObj:{},
				adderssType:'start',
				nowAddress:{
					location:{
						lng:'',
						lat:''
					}
				},
				releaseAddressObj:{},
				content:'',
			};
		},
		onLoad(e) {
			this.type=e.type
			uni.getLocation({
				type:'wgs84',
				success: (res) => {
					this.nowAddress={
						type:'now',
						location:{
							lng:res.longitude,
							lat:res.latitude
						}
					}
				}
			})
			
		},
		onShow() {
			
		},
		methods:{
			optionHandle(type){
				this.showOption=true
				this.optionType=type
				switch(type){
					case 'ageName':
						this.optionsTitle='请选择所需的驾驶年龄'
						this.options=[
							{name:'半年'},
							{name:'1年'},
							{name:'2年'},
							{name:'3年'},
						]
						break;
					case 'levelName':
						this.optionsTitle='请选择所需的驾驶年龄'
						this.options=[
							{name:'A1'},
							{name:'A2'},
							{name:'A3'},
							{name:'A4'},
						]
						break;
					case 'back':
						this.optionsTitle='是否需要返程'
						this.options=[
							{name:'是'},
							{name:'否'},
						]
						break;
				}
			},
			selectOption(e){
				this[this.optionType]=e.name
				this.showOption=false
			},
			chooseAddress(type){
				if(type=='start' && this.startAddressInfo){
					this.navTo('/pagesB/chooseAddress/index?data='+this.startAddressInfo)
					return
				}
				if(type=='dest' && this.destAddressInfo){
					this.navTo('/pagesB/chooseAddress/index?data='+this.destAddressInfo)
					return
				}
				
				this.navTo('/pagesB/chooseAddress/index?type='+type)
			},
			setAddress(data){
				if(data.type=='start'){
					this.startAddress=data.address+data.title+data.room
					this.startAddressObj=data
					this.startAddressObj.nowAddress=this.nowAddress
					this.startAddressInfo=JSON.stringify(data)
				}else{
					this.destAddress=data.address+data.title+data.room
					this.destAddressObj=data
					this.destAddressObj.startAddressObj=this.startAddressObj
					this.destAddressInfo=JSON.stringify(data)
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
.release-wrap{
	padding-bottom: 100upx;
	.form-wrap{
		background-color: #fff;
		/deep/ .u-form-item__body{
			padding:20upx 32upx;
		}
		.inp-view{
			text-align: right;
			height: 100%;
			color: #303133;
			font-size: 30upx;
			margin-right: 10upx;
			justify-content: flex-end;
		}
	}
	.map-wrap{
		padding: 30upx;
		.map-box{
			.title{
				position: relative;
				padding-left: 50upx;
				margin-bottom: 20upx;
				&::after{
					content: "";
					display: block;
					position: absolute;
					width: 24upx;
					height: 24upx;
					left: 0;
					top: 50%;
					transform: translateY(-50%);
					background-color: #1be053;
					border-radius: 50%;
				}
				&.dest::after{
					background-color:#e32818;
				}
			}
			
		}
		
	}
	.task-wrap{
		padding: 30upx;
		.tit{
			margin-bottom: 10upx;
		}
		.o-img{
			width: 35upx;
			height: 35upx;
		}
	}
	.btn-wrap{
		display: flex;
		justify-content: center;
		align-items: center;
		.btn{
			width: 430upx;
			height: 84upx;
			border-radius: 8upx;
			background-color: $base-color;
			color: #fff;
			font-size:40upx;
			text-align: center;
			line-height: 84upx;
		}
	}
}
</style>
