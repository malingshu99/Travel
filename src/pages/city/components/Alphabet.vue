<template>
	<!-- ref帮助我们获取dom -->
	<div class="list" ref="wrapper">
		<ul>
			<!-- 右侧导航 -->
			<li class="item" v-for='item of letters'
							 :key='item' 
							 :ref='item'
							 @click='handleLetterClick'
							 @touchstart='handleTouchStart'
							 @touchmove='handleTouchMove'
							 @touchend='handleTouchEnd'>{{item}}</li>
			
		</ul>
	</div>
</template>
<script>
import Bscroll from 'better-scroll'
	export default{
		name:'CityAlphabet',
		props:{
			cities:Object
		},
		computed:{
			letters () {
				const letters=[]
				for(let i in this.cities){
					letters.push(i)
				}
				return letters
			}
		},
		data () {			
			return{
				touchStatus:false,
				startY:0,
				timer:null
			}
		},
		//页面更新完成渲染之后开始执行  性能优化
		update () {
			this.startY = this.$refs['A'][0].offsetTop
		},
		methods:{
			handleLetterClick(e){
				//向外触发这个事件  等待监听
				this.$emit('change',e.target.innerText)
				// console.log(e.target.innerText)
			},
			handleTouchStart(){
				this.touchStatus = true
			},
			handleTouchMove(e){
				if(this.touchStatus){
					if(this.timer){
						clearTimeout(this.timer)
					}
					//正在执行同样事情的时候,延迟16ms之后再去执行,在这16ms中在此执行同样操作,则会把上一次执行的操作清除掉,重新执行这次执行的事情,减少handleTouchMove函数执行的频率,提高网页性能
					this.timer = setTimeout(()=>{
						// 第0项才是dom元素   计算'A'到Search.vue底部的距离
						// const startY = this.$refs['A'][0].offsetTop
						//得到手指到Search.vue底部的距离
						const touchY = e.touches[0].clientY-79
						//得到手指滑动的位置对应的下标是多少
						const index = Math.floor((touchY-this.startY)/20)
						if(index>= 0 && index<this.letters.length){
						this.$emit('change',this.letters[index])
					}
				},8)
				}
			},
			handleTouchEnd(){
				this.touchStatus = false
			}

		}
		
	}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'
	.list
		display:flex
		flex-direction:column
		justify-content:center
		position:absolute
		top:1.58rem
		right:0
		bottom:0
		width:.4rem
		.item
			color:$bgColor
			text-align:center
			line-height:.44rem

</style>