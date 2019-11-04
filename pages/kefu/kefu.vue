<template>
	<view>
		
		<view class="myRowlist">
			<view class="pubColor PubTit">在线咨询</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon1.png" mode=""></image></view>
				<view class="rr">029-38315662</view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon2.png" mode=""></image></view>
				<view class="rr">在线客服</view>
			</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="myRowlist">
			<view class="pubColor PubTit">在线预约</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon3.png" mode=""></image></view>
				<view class="rr"><input type="text" value="" placeholder="请输入姓名" /></view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon4.png" mode=""></image></view>
				<view class="rr"><input type="number" value="" placeholder="请输入联系方式" /></view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon5.png" mode=""></image></view>
				<view class="rr"><input type="text" value="" placeholder="请输入联系微信/QQ" /></view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon6.png" mode=""></image></view>
				<view class="rr"><input type="text" value="" placeholder="请输入您的预约信息···" /></view>
			</view>
		</view>
		
		<view class="submitbtn" style="margin-top: 100rpx;">
			<button class="">提交</button>
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
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">资讯</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/kefu/kefu'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar4-a.png" />
				</view>
				<view class="text this-text">客服</view>
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
			}
		},
		
		onLoad(options) {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
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
	
	.PubTit{padding: 20rpx 4%;color: #FF552E;}
	.myRowlist .item{padding: 26rpx 8%;border-top: 2rpx solid #eee;}
	.myRowlist .item .icon{width: 46rpx; height: 46rpx; display: block;margin-right: 30rpx;}
	.myRowlist .item .rr{width: 85%;}
	.myRowlist .item .rr input{width: 100%; display: block;line-height: 24rpx;font-size: 28rpx;}
</style>
