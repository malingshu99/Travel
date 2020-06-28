<template>
	<!-- ref帮助我们获取dom 使用ref属性为元素或组件添加标记，然后通过this.$refs获取-->
	<div class="list" ref="wrapper">
		<div>
			<div class="area">
					<div class="title border-topbottom">当前城市</div>
					<div class="button-list">
						<div class="button-wrapper">
							<div class="button">{{this.currentCity}}</div>
						</div>
					</div>
				</div>
				<div class="area">
					<div class="title border-topbottom">热门城市</div>
					<div class="button-list">
						<div class="button-wrapper"
							 v-for='item of hot' 
							 :key='item.id'
							 @click='handleCityClick(item.name)'>
							<div class="button">{{item.name}}</div>
						</div>
						
					</div>
				</div>



				<div class="area" v-for='(item,key) of cities' 
								  :key='key'
								  :ref='key'>
								  <!-- 使用ref属性为元素或组件添加标记，然后通过this.$refs获取 -->
					<div class="title border-topbottom">{{key}}</div>
					<div class="item-list">
						<div class="item border-bottom" 
							 v-for='innerItem of item' 
							 :key='innerItem.id'
							 @click='handleCityClick(innerItem.name)'
							 >{{innerItem.name}}</div>
						
					</div>
				</div>
				
			</div>
		
	</div>
</template>
<script>
import Bsroll from 'better-scroll'
import {mapState,mapMutations} from 'vuex'
	export default{
		name:'CityList',
		props:{
			cities:Object,
			hot:Array,
			letter:String
		},
		computed:{
			...mapState({
				// 映射属性,映射过来的名字为currentCity
				currentCity:'city'
			})
		},
		methods:{
			handleCityClick(city){
				// this.$store.commit('changeCity',city)
				this.changeCity(city)
				this.$router.push('/')
				// alert(city)
			},
			...mapMutations(['changeCity'])
		},
		/*生命周期函数  dom挂载完毕执行  {click: true}能让列表城市被单击*/
		mounted () {
			// Bsroll用到的必须是一个dom元素
			this.scroll = new Bsroll(this.$refs.wrapper,{click: true})
		},
		// zhemtingqi
		watch:{
			letter () {
				// letter不为空
				if(this.letter){
					// 使用ref属性为元素或组件添加标记，然后通过this.$refs获取,循环得到的ref得到的是一个数组
					const element = this.$refs[this.letter][0]
					this.scroll.scrollToElement(element)
					// console.log(element)
				}
				
			}	
		}
		
	}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.border-topbottom
	&:before
		border-color:#ccc
	&:after
		border-color:#ccc
. border-bottom
	&:before
		border-color:#ccc
.list
/*溢出隐藏多余的用下拉框*/
	overflow:hidden
	position:absolute
	top:1.58rem
	left:0
	right:0
	bottom:0
	
	.title
		line-height:.54rem
		background:#eee
		padding-left:.26rem
		color:#666
	.button-list
		padding:.1rem .6rem .1rem .1rem
		overflow:hidden
		.button-wrapper
			float:left
			width:33.3%
			.button
				margin:.1rem
				padding:.1rem 0
				text-align:center
				border:.02rem solid #ccc
				border-radius:.06rem
	.item-list
		.item
			line-height:.76rem
			
			padding:.2rem
</style>