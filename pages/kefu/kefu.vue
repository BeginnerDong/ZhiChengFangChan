<template>
	<view>
		
		<view class="myRowlist">
			<view class="pubColor PubTit">在线咨询</view>
			<view class="item flex" @click="phoneCall()">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon1.png" mode=""></image></view>
				<view class="rr">{{mainData.small_title}}</view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon2.png" mode=""></image></view>
				<button open-type="contact" style="line-height: 1;" class="rr">在线客服</button>
			</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="myRowlist">
			<view class="pubColor PubTit">在线预约</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon3.png" mode=""></image></view>
				<view class="rr"><input type="text" value="" placeholder="请输入姓名" v-model="submitData.name"/></view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon4.png" mode=""></image></view>
				<view class="rr"><input type="number" value="" placeholder="请输入联系方式" v-model="submitData.telphone"/></view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon5.png" mode=""></image></view>
				<view class="rr"><input type="text" value="" placeholder="请输入联系微信/QQ" v-model="submitData.qqwechat"/></view>
			</view>
			<view class="item flex">
				<view class="ll"><image class="icon" src="../../static/images/kefu-icon6.png" mode=""></image></view>
				<view class="rr"><input type="text" value="" placeholder="请输入您的预约信息···" v-model="submitData.content"/></view>
			</view>
		</view>
		
		<view class="submitbtn" style="margin-top: 100rpx;">
			<button class="" @click="Utils.stopMultiClick(submit)">提交</button>
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
				Utils:this.$Utils,
				mainData:[],
				submitData:{
					name:'',
					telphone:'',
					qqwechat:'',
					content:''
				}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);	
				var newObject = self.$Utils.cloneForm(self.submitData);
				const pass = self.$Utils.checkComplete(newObject);
				if (pass) {								
					self.messageAdd();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
					console.log(self.submitData)
				};
			},
			
			
			messageAdd() {
				const self = this;
				const postData = {};
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				console.log('postData',postData)			
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('预约提交成功', 'none');
						self.submitData = {
							name:'',
							telphone:'',
							qqwechat:'',
							content:''
						};
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.JustaddMessage(postData, callback);
			},
			
			phoneCall() {
				const self = this;
				wx.makePhoneCall({
					phoneNumber: self.mainData.small_title,
				})
			},
			
			getMainData() {
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
						self.mainData=res.info.data[0];
					};
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
	button{
		background: none;
		line-height: 1.5;
		text-align: left;
		font-size:14px
	}
	button::after{
		border: none;
	}
	.button-hover{
		color: #000000;
		background: none;
	}
	.PubTit{padding: 20rpx 4%;color: #FF552E;}
	.myRowlist .item{padding: 26rpx 8%;border-top: 2rpx solid #eee;}
	.myRowlist .item .icon{width: 46rpx; height: 46rpx; display: block;margin-right: 30rpx;}
	.myRowlist .item .rr{width: 85%;}
	.myRowlist .item .rr input{width: 100%; display: block;line-height: 24rpx;font-size: 28rpx;}
</style>
