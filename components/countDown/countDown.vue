<template>
	<view>
		{{countDownTime}}
	</view>
</template>

<script>
	export default {
		name:"countDown",
		props:{
			time
		},
		data() {
			return {
				countDownTime:''
			};
		},
		created() {
			this.countDown(this.time)
		},
		
		methods:{
			countDown(time) {
				console.log(1111,time)
				var nowTime = +new Date(); //返回当前时间总的毫秒数
				var inputTime = +new Date(time); //返回用户输入时间总毫秒数
				var times = (inputTime - nowTime) / 1000; //剩余时间总的秒数
				//转换时分秒
				var d = parseInt(times / 60 / 60 / 24);
				var h = parseInt(times / 60 / 60 % 24);
				var m = parseInt(times / 60 % 60);
				var s = parseInt(times % 60);
				console.log(12121212,times)
				if(times>0){
					console.log(12121212)
					this.countDownTime=`${d}天 ${h}:${m}:${s}`
					setTimeout(this.countDown(inputTime-1000), 1000)
				}else{
					this.countDownTime=`已结束`
				}
				
				
			},
		}
	}
</script>

<style lang="scss">

</style>