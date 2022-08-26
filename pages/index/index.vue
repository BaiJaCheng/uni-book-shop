<template>
	<view >
		<u-swiper :list="slides" name="img_url" height="350"></u-swiper>
		
		<view class="u-text-center u-m-t-20">
			<u-tabs-swiper ref="tabs" bar-width='100' item-width='160' :list="sortList"  :is-scroll="false" :current='currentSort'  @change='changeSort'></u-tabs-swiper>
		</view>
		
		<view class="wrap">
				<u-row gutter="16" class="u-skeleton">
					<u-col span="6" v-for="goods in goodsList.length !==0 ? goodsList : [{},{},{},{}] ">
					
						<goodsCard :goods="goods"></goodsCard>
					
					</u-col>
				</u-row>
				<!-- 骨架屏 -->
				<u-skeleton :loading="loading" :animation="true" bgColor="#FFF"></u-skeleton>
			</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sortList: [
					{name:'默认'},
					{name:'销量'},
					{name:'推荐'},
					{name:'最新'},
					],
					currentSort: 0,
					slides:[],
					goodsList:[],
					page:1,
					loading:false
			}
		},
		onLoad() {
		   this.getDate()
		},
		methods: {
			changeSort(current){
				this.currentSort = current
				console.log(this.currentSort)
				this.page = 1
				this.goodsList = []
				//判断筛选条件
				this.getDate()
			},
			//获取首页数据
			async getDate(){
				this.loading = true
				const params = {
					page:this.page,
				}
				if(this.currentSort == 1) params.sales = 1
				if(this.currentSort == 2) params.recommend = 1
				if(this.currentSort == 3) params.new = 1
						console.log(params)
				const res = await this.$u.api.index(params)
				this.loading = false
				this.slides = res.slides
				this.goodsList = [...this.goodsList,...res.goods.data]
			}
		},
		//触底事件
		onReachBottom() {
			//重新请求页面 
			this.page = this.page + 1
			this.getDate()
		}
	}
</script>

<style lang="scss" scoped>
	
</style>
