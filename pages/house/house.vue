<template>
	<view>
		<view class="navLisBox borderB1">
			<scroll-view class="scrollX" scroll-x>
				<!-- 点击导航选中当前项 -->
				<view class="nav-item" :class="curr==index?'on':''"  v-for="(item,index) in classify" :key="index" @click="change(index)">{{item}}</view>
			</scroll-view>
		</view>
		
		<view class="proList flexRowBetween">
			<view class="item-lis" v-for="(item,index) in produtList" :key="index" @click="Router.navigateTo({route:{path:'/pages/houseDetail/houseDetail'}})">
				<view>
					<image class="img" src="../../static/images/housing-img.png" alt="" />
				</view>
				<view class="infor">
					<view class="tit avoidOverflow">科技路地铁口 尚中心</view>
					<view class="flexRowBetween font12 ">
						<view class="color9 font10 text2 avoidOverflow">2室1厅 整租</view>
						<view class="money flexEnd">2400</view>
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
				curr:0
			}
		},
		
		onLoad(options) {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			change(index){
				const self = this;
				self.curr = index
			},
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
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
