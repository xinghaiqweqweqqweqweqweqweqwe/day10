<template>
	<view>
		<view class="homea">
			<input type="text" placeholder="输入关键词搜索">
		</view>
		<view class="">
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item,index) in list" :key="index">
					<image :src="item.picUrl" class="swiperList"></image>
				</swiper-item>
			</swiper>
		</view>
		<view class="">
			<h2>商品列表</h2>
			<view class="resultList">
				<view class="resultLista" v-for="(item,index) in arr" :key="index">
					<image :src="item.pic" mode=""></image>
					<h4>{{item.name}}</h4>
					<view>
						<span class="aa">￥{{item.minPrice}}</span>
						<span class="bb">￥{{item.originalPrice}}</span>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[],
				arr:[]
			};
		},
		mounted(){
			uni.$http.get('https://api.it120.cc/hjl/banner/list').then(res=>{
				this.list=res.data.data
			})
			uni.$http.post('https://api.it120.cc/hjl/shop/goods/list/v2').then(res=>{
				this.arr=res.data.data.result
			})
		}
	}
</script>

<style lang="scss">
.homea{
	input{
		height: 30px;
		width: 80%;
		border-radius: 30px;
		background-color: rgb(246, 248, 250);
		margin-left: 10%;
		padding-left: 15px;
	}
}
.swiperList{
	width: 100%;
	height: 150px;
}
h2{
	text-align: center;
	margin-top: 10px;
}
.resultList{
	display: flex;
	flex-wrap: wrap;
	.resultLista{
		width: 45%;
		margin: 5px;
		border: 1px solid gray;
		border-radius: 5px;
		image{
			width: 100%;
		}
		.aa{
			color: red;
		}
		.bb{
			color: gray;
			text-decoration:line-through;
			margin-left: 15px;
		}
	}
}
</style>
