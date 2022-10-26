<template>
	<view>
		<div class="search">
			<span>天使童装</span>
			<input type="text" placeholder="输入关键字搜索" @click="enter">
		</div>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods: {
			enter() {
				this.$emit('myclick')
			}
		},
	}
</script>

<style lang="scss">
.search{
	background-color: white;
	height: 100rpx;
	display: flex;
	span{
		font-size: 40rpx;
		font-weight: 800;
		padding: 0rpx 40rpx;
	}
	input{
		background-color: rgb(246,248,250);
	}
}
</style>
