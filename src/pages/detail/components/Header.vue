<template>
	<div>
		<router-link tag='div'
					 to='/' 
					 class="header-abs"
					 v-show='showAbs'>
			<div class="iconfont header-abs-back">&#xe624;</div>
		</router-link>
		<div class="header-fixed" 
			 v-show='!showAbs'
			 :style='opacityStyle'>
			<router-link to='/'>
				<div class="iconfont header-back">&#xe624;</div>
			</router-link>
			景点详情
		</div>
	</div>
</template>
<script>
	export default{
		name:'DetailHeader',
		data(){
			return {
				showAbs:true,
				opacityStyle:{
					opacity:0
				}
			}
		},
		methods:{
			// 景点详情的出现时间
			handleScroll(){
				const top = document.documentElement.scrollTop||document.body.scrollTop||window.pageYOffset
				if(top>60){
					let opacity = top/140
					// opacity最大值为1
					opacity = opacity > 1 ? 1 : opacity
					this.opacityStyle={
						opacity
					}
					this.showAbs=false
				}else{
					this.showAbs=true
				}
			}
		},
		mounted(){
			window.addEventListener('scroll',this.handleScroll)
		},
		//当页面即将更换的时候这个生命周期钩子将会被执行  对window时间进行解绑,只能在这个页面才有window事件
		destroyed(){
			window.removeEventListener('scroll',this.handleScroll)
		}
	}
</script>
<style lang='stylus' scoped>
	@import '~styles/varibles.styl'
	.header-abs
		position:absolute
		left:.2rem
		top:.2rem
		width:.8rem
		height:.8rem
		border-radius:.4rem
		background:rgba(0,0,0,.8)
		text-align:center
		line-height:.8rem
		.header-abs-back
			 color:#fff
			 font-size:.4rem
	.header-fixed
		position:fixed
		top:0
		left:0
		right:0
		z-index:2
		
		height:$headerHeight
		line-height:$headerHeight
		text-align:center
		color:#fff
		background:$bgColor
		font-size:.32rem
		.header-back
			position:absolute
			top:0
			left:0
			width:.64rem
			text-align:center
			font-size:.4rem
			color:#fff
</style>