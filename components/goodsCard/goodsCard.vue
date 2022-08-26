<template>

		<navigator class="goods-item">
			<u-image class="u-skeleton-fillet" width="100%" height="300rpx" :src="goods.cover_url"></u-image>
		
			<view class="title u-line-1 u-skeleton-rect">{{goods.title ? goods.title : '商品名称'}}</view>
			<view class="u-flex u-row-between">
				<view class="price u-skeleton-rect u-p-r-20">￥ {{goods.price}}</view>
				<view class="sales u-skeleton-rect">销量：{{goods.collects_count}}人</view>
			</view>
		</navigator>

</template>

<script>
	export default {
		name:"goodsCard",
		props:{
			goods:{
				typeof: Object,
				default(){
					 return {}
				}
			}
		},
		data() {
			return {
				
			};
		}
	}
</script>

<style scoped lang="scss">
	.goods-item{
		padding: 40rpx;
		margin-top: 30rpx;
		box-shadow: 0 12rpx 20rpx rgba(0, 0, 0, 0.1);
		.title{
			margin: 10rpx;
			font-weight: 500;
			font-size: 16px;
			width: 100%;
		}
		.price{
			color: red;
		}
		.sales{
			color: #888;
		}
	}
</style>