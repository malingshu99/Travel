<template>
<div class="wrapper">
	<swiper :options="swiperOption" v-if='showSwiper'>
	<!-- swiper的初次创建不是由空数组创建,让它由完整的数据创
	建当传递过来的list是一个空数组的时候,这时候v-if的值是false,swiper不会被创建,只有等
	到真正的数据来过之后才会被创建  (解决掉轮播图默认显示最后一页) -->
    <swiper-slide v-for='item of list' :key='item.id'>
		<img class='swiper-img' :src="item.imgUrl">
    </swiper-slide>
    <div class="swiper-pagination" slot="pagination"></div>
  </swiper>
</div>
</template>
<script>
/*v-bind就是用于绑定数据和元素属性的*/
export default{
	name:'HomeSwiper',
	props:{
		list:Array
	},
	// ES6写法
	data () {
		return {
				swiperOption:{
					/*导航圆点*/
					pagination:'.swiper-pagination',
					/*让轮播图循环*/
					loop:true
					}
				}
		},
		/*计算属性 返回list的长度*/
		computed:{
			showSwiper () {
				return this.list.length
			}
		}
}
</script>
<style lang="stylus" scoped>
/*穿透只要weapper后面有这个类就能显示出来 不受scoped的限制*/
.wrapper>>>.swiper-pagination-bullet-active
		background:#fff !important
.wrapper
	overflow:hidden
	width:100%
	height:0
	/*height一定为零 overflow:hidden 通过padding-bottom宽高百分比*/
	padding-bottom:30%
	.swiper-img
		width:100%

</style>