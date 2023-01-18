<template>
	<view class="coll-wrap">
		<navbar  @onRightClick="onRightClick" :mysNavConfig="mysNavConfig">
			<view class="nav-left" slot="left">
				<u-icon name="arrow-left" color="#fff" size="16"  ></u-icon>
			</view>
			<view class="nav-right" slot="right">
				编辑
			</view>
		</navbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mysNavConfig:{
					isHome:false,
					navPadding:true,	
					navFixed:true,
					btnType:'type1',
					bgColor:'#FB852D',
					navTitle:{
						text:'我的收藏',
						color:'#fff'
					}
				},
			};
		},
		methods:{
			onRightClick(){
				
			}
		}
	}
</script>

<style lang="scss" scoped>
.coll-wrap{
	
}
</style>
