<template>
	<view>
		<view class="index_topBj">
			<view class="banner-box">
				<view class="banner oh">
					<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="4000" duration="1000"  indicator-active-color="#fff">
						<block v-for="(item,index) in swiperData" :key="index">
							<swiper-item class="swiper-item">
								<image @click="Router.navigateTo({route:{path:item.url}})" 
								:src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="slide-image"/>
							</swiper-item>
						</block>
					</swiper>
				</view>
			</view>
		</view>
		
		<view class="indHome pdlr4 flexRowBetween pdb15">
			<view class="item"  @click="Router.navigateTo({route:{path:'/pages/house/house?id=1'}})">
				<image src="../../static/images/home-icon.png"></image>
				<view class="tit">推荐房源</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/house/house?id=2'}})">
				<image src="../../static/images/home-icon1.png"></image>
				<view class="tit">二手房</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/house/house?id=4'}})">
				<image src="../../static/images/home-icon2.png"></image>
				<view class="tit">出租房</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/kefu/kefu'}})">
				<image src="../../static/images/home-icon3.png"></image>
				<view class="tit">我要租房</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/house/house?id=5'}})">
				<image src="../../static/images/home-icon4.png"></image>
				<view class="tit">新房</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/house/house?id=6'}})">
				<image src="../../static/images/home-icon5.png"></image>
				<view class="tit">厂房</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/house/house?id=7'}})">
				<image src="../../static/images/home-icon6.png"></image>
				<view class="tit">商铺</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/kefu/kefu'}})">
				<image src="../../static/images/home-icon7.png"></image>
				<view class="tit">我要买房</view>
			</view>
		</view>
		
		<view class="f5H10"></view>
		<view class="pdtb15">
			<swiper class="swiper-box bannerTwo" indicator-dots="true" autoplay="true" interval="4000" duration="1000"  indicator-active-color="#fff">
				<block v-for="(item,index) in bannerData" :key="index">
					<swiper-item class="swiper-item">
						<image @click="Router.navigateTo({route:{path:item.url}})"
						:src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="slide-image"/>
					</swiper-item>
				</block>
			</swiper>
		</view>
		<view class="borderB1"></view>
		
		<view class="mglr4 pdtb10 borderB1">在线咨询</view>
		<view class="pdtb10 mglr4 kefuBox flexRowBetween">
			<view class="ll flex">
				<view>
					<image class="photo" :src="kfData.mainImg&&kfData.mainImg[0]?kfData.mainImg[0].url:''" mode=""></image>
				</view>
				<view class="infor color9 font11">
					<view class="name color2 font12 pdb5">{{kfData.title}}</view>
					<view>所属公司：{{kfData.keywords}}</view>
					<view>服务年限：{{kfData.description}}</view>
				</view>
			</view>
			<view class="rr flexEnd" @click="phoneCall()">
				<image class="iphone" src="../../static/images/home-icon8.png" mode=""></image>
			</view>
		</view>
		<view class="borderB1"></view>
		<view class="proList flexRowBetween">
			<view class="item-lis" v-for="(item,index) in mainData" :key="index" 
			@click="Router.navigateTo({route:{path:'/pages/houseDetail/houseDetail?id='+item.id}})">
				<view>
					<!-- <image class="img" src="https://www.zhicfangc.com/api/public/uploads/20190717/6f3c05369b5f9a84f5729a04ece4f513.jpg" alt="" /> -->
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
					<image src="../../static/images/nabar1-a.png" />
				</view>
				<view class="text this-text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/house/house'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">房源</view>
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
				labelData: [
					"../../static/images/home-banner1.png",
					"../../static/images/home-banner1.png",
				],
				bannerTwo: [
					"../../static/images/home-banner2.png",
					"../../static/images/home-banner2.png",
				],
				swiperData:[],
				mainData:[],
				kfData:{},
				bannerData:[]
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getSliderData','getMainData','getKeFuData','getBannerData'], self);
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
			
			phoneCall() {
				const self = this;
				wx.makePhoneCall({
					phoneNumber: self.kfData.small_title,
				})
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
					menu_id: 1,
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
							title: ['=', ['首页轮播']],
						},
						middleKey: 'parentid',
						key: 'id',
						condition: 'in',
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.swiperData.push.apply(self.swiperData, res.info.data)
					}
					console.log('self.swiperData', self.swiperData)
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getBannerData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
				};
				postData.getBefore = {
					caseData: {
						tableName: 'Label',
						searchItem: {
							title: ['=', ['首页广告']],
						},
						middleKey: 'parentid',
						key: 'id',
						condition: 'in',
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.bannerData.push.apply(self.bannerData, res.info.data)
					}
					console.log('self.bannerData', self.bannerData)
					self.$Utils.finishFunc('getBannerData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getKeFuData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
				};
				postData.getBefore = {
					caseData: {
						tableName: 'Label',
						searchItem: {
							title: ['=', ['客服']],
						},
						middleKey: 'menu_id',
						key: 'id',
						condition: 'in',
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.kfData=res.info.data[0];
					};
					self.$Utils.finishFunc('getKeFuData');
				};
				self.$apis.articleGet(postData, callback);
			},
		},
		
	};
</script>

<style>
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/proList.css";
	
	page{padding-bottom: 160rpx;}
	.swiper-box {height: 330rpx;box-sizing: border-box;overflow: hidden;}
	.swiper-box swiper-item {width: 100%;}
	.swiper-box image {width: 100%;height: 100%;}
	.swiper-box.bannerTwo{height: 270rpx; width: 702rpx;margin: 0 auto;}
	
	/* 分类导航 */
	.indHome{ flex-wrap:wrap;}
	.indHome .item{width: 25%;text-align: center;padding-top: 15px; font-size: 24rpx; color: #222;display: flex; flex-direction: column;}
	.indHome .item image {width:100rpx;height: 100rpx; border-radius: 50%;margin-bottom: 20rpx;margin: 0 auto 16rpx auto; }
	
	/* 在线咨询 */
	.kefuBox .ll{ width: 85%;}
	.kefuBox .ll .photo{width:106rpx; height: 106rpx;border-radius: 50%; display: block;}
	.kefuBox .ll .infor{margin-left: 20rpx;}
	.kefuBox .rr{width: 15%;}
	.kefuBox .rr .iphone{width:72rpx; height: 72rpx;display: block;}
	
</style>
