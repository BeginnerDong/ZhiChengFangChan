<template>
	<view>
		
		<view class="newsList pdlr4">
			<view class="item flexRowBetween borderB1" v-for="(item,index) in mainData" :key="index" 
			@click="Router.navigateTo({route:{path:'/pages/newsDetail/newsDetail?id='+item.id}})">
				<view class="ll">
					<view class="avoidOverflow2">{{item.title}}</view>
					<view class="color9 lable">智诚房产 <text class="data">{{item.create_time}}</text></view>
				</view>
				<view class="rr flexEnd">
					<image class="pic" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
				</view>
			</view>
		</view>
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1.png" />
				</view>
				<view class="text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/house/house'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">房源</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/news/news'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3-a.png" />
				</view>
				<view class="text this-text">资讯</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/kefu/kefu'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar4.png" />
				</view>
				<view class="text">客服</view>
			</view>
		</view>
		<!--底部tab键 end-->
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				Router: this.$Router,
				mainData: [],
			}
		},

		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
			
		},

		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},

		methods: {

			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 5
					}
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 2,
				};
				postData.getBefore = {
					caseData: {
						tableName: 'Label',
						searchItem: {
							title: ['=', ['资讯']],
						},
						middleKey: 'menu_id',
						key: 'id',
						condition: 'in',
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					} else {
						self.$Utils.showToast('没有更多了', 'none');
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		},
	};
</script>

<style>
	@import "../../assets/style/navbar.css";
	page{padding-bottom: 160rpx;}
	.newsList .item{padding: 30rpx 0; }
	.newsList .item .ll{width: 63%; height: 144rpx; position: relative;}
	.newsList .item .ll .lable{position: absolute;left: 0;bottom: 0;width: 100%;box-sizing: border-box; font-size: 24rpx;}
	.newsList .item .ll .lable .data{margin-left: 20rpx;}
	.newsList .item .rr{width: 35%;}
	.newsList .item .rr .pic{width: 200rpx; height: 144rpx; display: block;}
</style>
