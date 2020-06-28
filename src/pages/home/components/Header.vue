<template>
<!-- 只能暴露一个标签 -->
<div class="header">
	<div class="header-left">
		<div class="iconfont back-icon">&#xe624;</div>
	</div>
	<div class="header-input">
		<span class="iconfont">&#xe632;</span>
		输入城市/景点/游玩主题
	</div>
	<router-link to='/city'>
		<div class="header-right">
			<!-- 调用store -->
			<!-- {{this.$store.state.city}} -->
			{{this.city}}
			<span class="iconfont arrow-icon">&#xe64a;</span>
		</div>
		
	</router-link>
</div>
</template>	
<script>
import {mapState} from 'vuex'
// import {mapState,mapGetters} from 'vuex'
export default{
	name:'HomeHeader',
	// props:{
	// 	city:String
	// }
	computed:{
		//mapState把vuex中的数据映射到计算属性中
		...mapState(['city'])
		// ...mapGetters(['doubleCity'])
	}
}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'

/*@import './../../../assets/styles/varibles.styl'*/
.header
	display:flex
	line-height:$headerHeight
	background:$bgColor
	color:#fff

	.header-left
		width:.64rem
		float:left
		.back-icon
			text-align center
			font-size .4em
	.header-input
		flex:1
		height:.64rem
		line-height:.64rem
		color:#ccc
		margin-top:.12rem
		margin-left:.2rem
		background:#fff
		border-radius:.1rem
		padding-left .2rem

	.header-right
		min-width:1.04rem
		padding:0 .1rem
		float:right
		text-align:center
		color:#fff
		.arrow-icon
			font-size .24rem
			margin-left -.04rem
</style>