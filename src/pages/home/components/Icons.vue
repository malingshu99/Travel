<template>
<div class="icons">
<swiper :options="swiperOption">
<swiper-slide v-for='(page,index) of pages'  :key='index'>
	<!-- 用循环遍历 -->
	<div class="icon" v-for='item of page' :key='item.id'>
		<div class="icon-img">
			<img class="icon-img-content" :src="item.imgUrl" />
		</div>
	<p class='icon-dec'>{{item.desc}}</p>
	</div>
</swiper-slide>
</swiper>
</div>
</template>
<script>
	export default{
		name:'HomeIcons',
		props:{
			list:Array
		},
		data () {
			// 不让自动滚动
			return{
				swiperOption:{
				autoplay:false
			}
			}
			
		},
		// 定义计算属性  根据其他的属性计算出来生成一组新的结果 自带缓存机制 语法简单
		computed:{
			pages () {
				const pages = []
				this.list.forEach((item,index)=>{
					// 当前数据对应的下标应该显示在第几页
					const page = Math.floor(index/8)
					if(!pages[page]){
						pages[page]=[]
					}
					pages[page].push(item)
				})
				return pages
			}
		}
	}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'
@import '~styles/mixins.styl'
	.icons>>>.swiper-container
			height:0
			padding-bottom:50%
	.icons
		margin-top:.1rem
		.icon

			position:relative
			overflow:hidden
			float:left
			width:25%
			height:0
			padding-bottom:25%
			
			.icon-img
				position:absolute
				top:0
				left:0
				right:0
				bottom:.44rem
				
				box-sizing:border-box
				padding:.1rem
				.icon-img-content
					display:block
					margin:0 auto
					height:100%
			.icon-dec
				position:absolute
				right:0
				left:0
				bottom:0
				height:.44rem
				line-height:.44rem
				color:$darkTextColor
				text-align:center
				/*当文字特别多的时候后面以...代替*/
				ellipsis()
</style>