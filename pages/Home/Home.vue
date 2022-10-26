<template>
	<view class="">
		<scroll-view @scroll="gd" scroll-y>
			<view class="homea" :class="{zz:qh}">
				<view class="a">
					天使童装
				</view>
				<view class="b" @click="enter">
					输入关键字搜索
				</view>
			</view>
			<view class="">
				<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
					<swiper-item v-for="(item, index) in list" :key="index">
						<image :src="item.picUrl" class="swiperList"></image>
					</swiper-item>
				</swiper>
			</view>
			<view class="">
				<h2>商品列表</h2>
				<view class="resultList">
					<view class="resultLista" v-for="(item, index) in arr" :key="index">
						<image :src="item.pic" mode=""></image>
						<h4>{{ item.name }}</h4>
						<view>
							<span class="aa">￥{{ item.minPrice }}</span>
							<span class="bb">￥{{ item.originalPrice }}</span>
						</view>
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				arr: [],
				qh:false
			};
		},
		mounted() {
			uni.$http.get('https://api.it120.cc/hjl/banner/list').then(res => {
				this.list = res.data.data;
			});
			uni.$http.post('https://api.it120.cc/hjl/shop/goods/list/v2').then(res => {
				this.arr = res.data.data.result;
			});
		},
		methods: {
			enter() {
				// console.log('ok');
				uni.navigateTo({
					url: '/subpkg/search/search'
				});
			},
			gd() {
				console.log(123);
			}
		},
		onPageScroll(a) {
			if(a.scrollTop>0){
				this.qh=true
			}else{
				this.qh=false
			}
		}
	};
</script>

<style lang="scss">
	.homea {
		display: flex;
		height: 40px;
		background-color: #fff;
		width: 100%;
		align-items: center;
		margin-bottom: 10px;
		z-index: 1000000;

		.a {
			font-size: 14px;
			margin-left: 10px;
		}

		.b {
			padding-left: 15px;
			margin-left: 10px;
			background-color: #f0f0f0;
			border-radius: 10px;
			width: 180px;
		}
	}

	.zz {
		position: fixed;
	}

	.swiperList {
		width: 100%;
		height: 150px;
	}

	h2 {
		text-align: center;
		margin-top: 10px;
	}

	.resultList {
		display: flex;
		flex-wrap: wrap;

		.resultLista {
			width: 45%;
			margin: 5px;
			border: 1px solid gray;
			border-radius: 5px;

			image {
				width: 100%;
			}

			.aa {
				color: red;
			}

			.bb {
				color: gray;
				text-decoration: line-through;
				margin-left: 15px;
			}
		}
	}

	.search {
		background-color: white;
		height: 100rpx;
		display: flex;

		span {
			font-size: 40rpx;
			font-weight: 800;
			padding: 0rpx 40rpx;
		}

		input {
			background-color: rgb(246, 248, 250);
		}
	}
</style>
