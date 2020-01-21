<template>
	<view>
		<view class="navLisBox borderB1">
			<scroll-view class="scrollX" scroll-x>
				<!-- 点击导航选中当前项 -->
				<view class="nav-item" :class="curr==item.id?'on':''"  v-for="(item,index) in swiperData" 
				:key="index" @click="change(item.id)">{{item.title}}</view>
			</scroll-view>
		</view>
		
		<view class="proList flexRowBetween">
			<view class="item-lis" v-for="(item,index) in mainData" :key="index" 
			@click="Router.navigateTo({route:{path:'/pages/houseDetail/houseDetail?id='+item.id}})">
				<view>
					<image class="img" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" alt="" />
				</view>
				<view class="infor">
					<view class="tit avoidOverflow">{{item.title}}</view>
					<view class="flexRowBetween font12 ">
						<view class="color9 font10 text2 avoidOverflow">{{item.layout}}</view>
						<view class="money flexEnd">{{item.price}}</view>
					</view>
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
					<image src="../../static/images/nabar2-a.png" />
				</view>
				<view class="text this-text">房源</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/news/news'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">资讯</view>
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
				Router:this.$Router,
				showView: false,
				wx_info:{},
				classify:['推荐房源','二手房','出租房','新房','厂房','商铺'],
				produtList:[{},{},{},{},{},{},{},{}],
				curr:'',
				swiperData:[],
				mainData:[]
			}
		},
		
		onLoad(options) {
			const self = this;
			if(options.id){
				console.log(323)
				self.id = options.id
			};
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getSliderData'], self);
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
			
			change(id){
				const self = this;
				self.curr = id;
				self.getMainData(true);
			},
			
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
					menu_id: self.curr,
				};
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			getSliderData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
				};
				postData.getBefore = {
					caseData: {
						tableName: 'Label',
						searchItem: {
							title: ['=', ['房屋类型']],
						},
						middleKey: 'parentid',
						key: 'id',
						condition: 'in',
					},
				};
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.swiperData.push.apply(self.swiperData, res.info.data);
						if(self.id){
							self.curr = self.id
						}else{
							self.curr = self.swiperData[0].id;
						}
						
						self.getMainData()
					}
					console.log('self.swiperData', self.swiperData)
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			
		},
	};
</script>

<style>
	@import "../../assets/style/proList.css";
	@import "../../assets/style/navbar.css";
	
	page{padding-bottom: 160rpx;}
	.navLisBox{ padding:10rpx 4%;}
	.navLisBox .scrollX{white-space: nowrap; }
	.navLisBox .nav-item{line-height: 60rpx; font-size: 28rpx; display: inline-block;width: 28%;text-align: center;}
	.navLisBox .nav-item.on{ color: #FF552E;}
</style>
