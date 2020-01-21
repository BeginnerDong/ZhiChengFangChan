<template>
	<view>
		
		<view class="mglr4 pdtb15">
			<view class="font16">{{mainData.title}}</view>
			<view class="color9 lable font12 pdt10 flex">
				<view class="">来源：智诚房产</view>
				<view class="data">发布时间：{{mainData.create_time}}</view>
			</view>
		</view>
		<view class="">
			<image style="width: 100%; height: 330rpx;" :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''" mode=""></image>
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
	page{padding-bottom: 60rpx;}
	.lable .data{margin-left: 40rpx;}
	.xqInfor {padding: 20rpx 4%; line-height: 40rpx;}
	.xqInfor .cont view {font-size: 26rpx;line-height: 44rpx;padding-bottom: 10rpx;}
	.xqInfor .cont .title{font-size: 28rpx; color: #333;}
	.xqInfor .cont image{max-width: 100% !important; display: block;margin: 20rpx auto;}
</style>
