<template>
	<view class="searchs">
		<header>
			<div class="input">
				<uni-icons class="icon" type="search" size="20"></uni-icons>
				<input type="text" placeholder="请输入搜素关键字" v-model="value" @input="ss" />
			</div>
		</header>
		<nav v-show="value.length == 0">历史搜素</nav>
		<view class="aa">
			<ul v-show="value.length == 0">
				<li v-for="(item, index) in historyList" :key="index">
					<span>{{ item }}</span>
					<button @click="sc(index)">删除&nbsp;×</button>
				</li>
			</ul>
		</view>
		<view class="box" v-show="value.length != 0">
			<ul>
				<li>综合</li>
				<li>新品</li>
				<li>销量</li>
				<li>价格</li>
			</ul>
			<view class="small" v-for="(item, index) in cartList" :key="index">
				<div class="left"><img :src="item.pic" alt="" /></div>
				<div class="right">
					<span>{{ item.name }}</span>
					<span>{{item.characteristic}}</span>
					<span>
						<span>￥{{item.minPrice}}</span>
						<span>￥{{item.originalPrice}}</span>
					</span>
					<span>已售出{{item.numberSells}}件</span>
				</div>
				<div class="zr">
					<uni-icons type="cart" size="40" color="red"></uni-icons>
				</div>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			historyList: JSON.parse(uni.getStorageSync('history') || '[]'),
			value: '',
			cartList: '',
			time: ''
		};
	},
	methods: {
		ss() {
			clearTimeout(this.time);
			this.time = setTimeout(async () => {
				this.historyList.unshift(this.value);
				let { data: res } = await uni.$http.post('https://api.it120.cc/hjl/shop/goods/list/v2?nameLike=' + this.value);
				// console.log(res);
				this.cartList = res.data.result;
				console.log(this.cartList);
			}, 500);
		},
		sc(index) {
			this.historyList.splice(index, 1);
		}
	},
	watch: {
		historyList() {
			uni.setStorageSync('history', JSON.stringify(this.historyList));
		}
	},
	onLoad() {
		console.log(this.historyList);
	}
};
</script>

<style lang="scss">
html body .searchs {
	background-color: white;
	height: 800rpx;
}
header {
	background-color: white;
	display: flex;
	padding-top: 10px;
	.input {
		background-color: rgb(246, 248, 250);
		width: 90%;
		margin: auto;
		height: 60rpx;
		display: flex;
		align-items: center;
		.icon {
			background-color: rgb(246, 248, 250);
			height: 20px;
			margin-left: 10px;
			width: 30px;
		}
		input {
			flex: 1;
		}
	}
}
nav {
	margin-left: 40rpx;
	margin-top: 20rpx;
}
.aa ul {
	padding: 0;
	li {
		display: flex;
		list-style: none;
		border-top: 1px solid darkgray;
		padding: 10px 30px;
		align-items: center;
		// justify-content: space-between;
		button {
			width: 70px;
			font-size: 12px;
			margin-right: 10px;
			float: right;
			color: white;
			background-color: rgb(25, 137, 250);
		}
	}
}
li {
	list-style: none;
}
.box {
	ul {
		display: flex;
		justify-content: space-around;
	}
	.small {
		margin-top: 20rpx;
		display: flex;
		justify-content: space-between;
		.left {
			img {
				width: 300rpx;
				height: 300rpx;
			}
		}
		.right {
			margin-right: 20rpx;
			display: flex;
			flex-direction: column;
			span:nth-of-type(1){
				color: black;
				margin-top: 10rpx;
				margin: 20rpx 0;
			}
			span:nth-of-type(2){
				color: darkgray;
				font-size: 28rpx;
			}
			span:nth-of-type(3){
				margin: 20rpx 0;
				span:nth-of-type(1){
					color: red;
					margin-right: 10rpx;
				}
				span:nth-of-type(2){
					color: darkgray;
					font-size: 28rpx;
					text-decoration: line-through;
				}
			}
			span:nth-of-type(4){
				color: darkgray;
				font-size: 28rpx;
			}
		}
		.zr{
			display: flex;
			align-items: flex-end;
			.icons{
				color: red;
			}
		}
	}
}
</style>
