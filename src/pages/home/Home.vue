<template>
<!-- 只能暴露一个标签 -->
<div>
<!-- 父组件向子组件传值通过属性的方式 -->
<home-header></home-header>
<home-swiper :list='swiperList'></home-swiper>
<home-icons :list='iconList'></home-icons>
<home-recommend :list='recommendList'></home-recommend>
<home-weekend :list='weekendList'></home-weekend>
	
</div>
</template>	
<script>
import HomeHeader from './components/Header.vue'
import HomeSwiper from './components/Swiper.vue'
import HomeIcons from './components/Icons.vue'
import HomeRecommend from './components/Recommend.vue'
import HomeWeekend from './components/Weekend.vue'
//用axios来发送ajax请求
//只有static里面的内容能被外部访问到
//.gitignore中定义后mock就不回提交到线上仓库
import axios from 'axios'
import {mapState} from 'vuex'
export default{
	name:'Home',
	components:{
		HomeHeader,
		HomeSwiper,
		HomeIcons,
		HomeRecommend,
		HomeWeekend
	},
	data () {
		return {
			// city:'',
			swiperList:[],
			iconList:[],
			recommendList:[],
			weekendList:[],
			lastCity:''
		}
	},
	computed:{
		...mapState(['city'])
	},
	methods:{
		getHomeInfo(){
			//本地模拟接口地址  
			// axios.get('/static/mock/index.json')
			// 上线   config下index.js  请求的时候api会自动替换
			axios.get('/api/index.json?city'+this.city)
			.then(this.getHomeInfoSucc)
		},
		getHomeInfoSucc(res){
			// 拿到ajax数据内容
			res = res.data
			if(res.ret&&res.data){
				// 定义一个变量
				const data = res.data
				// this.city = data.city
				// this.city = res.data.city

				this.swiperList = data.swiperList
				this.iconList = data.iconList
				this.recommendList = data.recommendList
				this.weekendList = data.weekendList

			}
		}
	},
	//生命周期函数 
	//每次切换到这个组件 mounted这个属性就会被重新执行  ajax数据就会被重新获取
	mounted(){
		//页面挂载完毕后执行getHomeInfo函数
		this.lastCity = this.city
		this.getHomeInfo();
	},
	activated(){
		// 发现上一次和本次的不同的时候
		if(this.lastCity!==this.city){
			this.lastCity = this.city
			this.getHomeInfo()
		}
	}
}

</script>
<style>
	
</style>