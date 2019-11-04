<template>
	<view>
		
		<view class="newsList pdlr4">
			<view class="item flexRowBetween borderB1" v-for="(item,index) in newsDate" :key="index" @click="Router.navigateTo({route:{path:'/pages/newsDetail/newsDetail'}})">
				<view class="ll">
					<view class="avoidOverflow2">长安区高效聚集，使其成为西安人居环境最好的区域之一。</view>
					<view class="color9 lable">智诚房产 <text class="data">2019-11-04</text></view>
				</view>
				<view class="rr flexEnd">
					<image class="pic" src="../../static/images/information-img.png" mode=""></image>
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
				Router:this.$Router,
				showView: false,
				wx_info:{},
				newsDate:[{},{},{},{},{},{},{}]
			}
		},
		
		onLoad(options) {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			change(curr){
				const self=this;
				if(curr!==self.curr){
					self.curr=curr
				}
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
	@import "../../assets/style/navbar.css";
	page{padding-bottom: 160rpx;}
	.newsList .item{padding: 30rpx 0; }
	.newsList .item .ll{width: 63%; height: 144rpx; position: relative;}
	.newsList .item .ll .lable{position: absolute;left: 0;bottom: 0;width: 100%;box-sizing: border-box; font-size: 24rpx;}
	.newsList .item .ll .lable .data{margin-left: 20rpx;}
	.newsList .item .rr{width: 35%;}
	.newsList .item .rr .pic{width: 200rpx; height: 144rpx; display: block;}
</style>
