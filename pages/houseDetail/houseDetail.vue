<template>
	<view>
		<view class="index_topBj">
			<view class="banner-box">
				<view class="banner oh">
					<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="4000" duration="1000"  indicator-active-color="#fff">
						<block v-for="(item,index) in mainData.mainImg" :key="index">
							<swiper-item class="swiper-item">
								<image  style="width: 100%;"
								:src="item.url?item.url:''" class="slide-image"/>
							</swiper-item>
						</block>
					</swiper>
				</view>
			</view>
		</view>
		
		<view class="font15 pdtb10 borderB1 mglr4">{{mainData.title}}</view>
		
		<view class="mglr4 pdtb15 detailData center flexRowBetween font13 color6">
			<view class="item">
				<view class="number">{{mainData.price}}</view>
				<view>售价</view>
			</view>
			<view class="item">
				<view class="number">{{mainData.layout}}</view>
				<view>房型</view>
			</view>
			<view class="item">
				<view class="number">{{mainData.area}}㎡</view>
				<view>面积</view>
			</view>
		</view>
		<view class="borderB1"></view>
		<view class="detailSpecs flexRowBetween font13">
			<view class="item pdb5">房间：主卧</view>
			<view class="item  pdb5">朝向：{{mainData.direction}}</view>
			<view class="item">楼层：{{mainData.floor}}</view>
			<view class="item">装修：{{mainData.decoration}}</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="pdlr4 borderB1">
			<view class="pdtb10">房源概况</view>
		</view>
		
		<view class="xqInfor">
			<view class="content ql-editor" v-html="mainData.content">
			</view>
		</view>
		
	
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router: this.$Router,


				mainData: {}
			}
		},

		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},

		methods: {

			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.searchItem = {
					id: self.id
				}
				const callback = (res) => {
					if (res.solely_code == 100000 && res.info.data[0]) {
						self.mainData = res.info.data[0];

						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
					} else {
						self.$Utils.showToast(res.msg, 'none')
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	}
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
