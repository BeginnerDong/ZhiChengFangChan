<template>
	<view>
		<view class="detailxqBan">
			<image src="../../static/images/details-banner.png" mode=""></image>
		</view>
		
		<view class="font15 pdtb10 borderB1 mglr4">科技路地铁口 尚中心 临近高新一中初中部 周边环境优美 交通便利 商业文化气息浓厚</view>
		
		<view class="mglr4 pdtb15 detailData center flexRowBetween font13 color6">
			<view class="item">
				<view class="number">2400元/月</view>
				<view>售价</view>
			</view>
			<view class="item">
				<view class="number">2室1厅1卫</view>
				<view>房型</view>
			</view>
			<view class="item">
				<view class="number">99㎡</view>
				<view>面积</view>
			</view>
		</view>
		<view class="borderB1"></view>
		<view class="detailSpecs flexRowBetween font13">
			<view class="item pdb5">房间：主卧</view>
			<view class="item  pdb5">朝向：南北</view>
			<view class="item">楼层：11层 (共23层)</view>
			<view class="item">装修：简装</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="pdlr4 borderB1">
			<view class="pdtb10">房源概况</view>
		</view>
		
		<view class="xqInfor">
			<view class="cont">
				<view>房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况房源概况。</view>
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
	page{border-bottom: 90rpx solid #F5F5F5;}
	.detailxqBan{width: 100%; height: 330rpx; display: block;}
	.detailxqBan image{ width: 100%; height: 100%; display: block;}
	
	.detailData .item{ width: 33.3%;}
	.detailData .item .number{color: #ff9600; font-size: 28rpx; margin-bottom: 10rpx;}
	.detailSpecs{flex-wrap: wrap;padding: 30rpx 6%;}
	.detailSpecs .item{width: 50%; box-sizing: border-box;}
	
	.xqInfor {padding: 20rpx 4%; line-height: 40rpx;}
	.xqInfor .cont view {font-size: 26rpx;line-height: 44rpx;padding-bottom: 10rpx;}
	.xqInfor .cont .title{font-size: 28rpx; color: #333;}
	.xqInfor .cont image{max-width: 100% !important; display: block;margin: 20rpx auto;}
</style>
