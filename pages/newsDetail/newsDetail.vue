<template>
	<view>
		
		<view class="mglr4 pdtb15">
			<view class="font16">长安区高效聚集，使其成为西安人居环境最好的区域之一。</view>
			<view class="color9 lable font12 pdt10 flex">
				<view class="">来源：智诚房产</view>
				<view class="data">发布时间：2019-11-04</view>
			</view>
		</view>
		<view class="">
			<image style="width: 100%; height: 330rpx;" src="../../static/images/details-banner.png" mode=""></image>
		</view>
		<view class="xqInfor">
			<view class="cont">
				<view>房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况。</view>
				<view>房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况。</view>
				<view>房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况。</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				wx_info:{}
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
	page{padding-bottom: 60rpx;}
	.lable .data{margin-left: 40rpx;}
	.xqInfor {padding: 20rpx 4%; line-height: 40rpx;}
	.xqInfor .cont view {font-size: 26rpx;line-height: 44rpx;padding-bottom: 10rpx;}
	.xqInfor .cont .title{font-size: 28rpx; color: #333;}
	.xqInfor .cont image{max-width: 100% !important; display: block;margin: 20rpx auto;}
</style>
