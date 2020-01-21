<template>
	<view>
		
		<view class="detailxqBan">
			<image :src="mainData.bannerImg&&mainData.bannerImg[0]?mainData.bannerImg[0].url:''" mode=""></image>
		</view>
		<view class="xqInfor mglr4 pdt20">
			<view class="title">
				<view class="center fs14">{{mainData.title}}</view>
				<!-- <view class="fs13 color6 pdt10 flexEnd" >{{mainData.description}}</view> -->
			</view>
			<view class="cont pdt15 fs13">
				<view class="content ql-editor" style="padding:0;"
				v-html="mainData.content">
				</view>
			</view>
		</view>
		
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:{}
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
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					id: self.id
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/personList.css";
	
	page{padding-bottom:60rpx;}
	
	.detailxqBan{ width: 100%;height: 400rpx; display: block;}
	.detailxqBan image{ width: 100%; height: 100%; display: block;}
	
	.xqInfor .cont image{max-width: 100% !important; display: block;margin:20rpx auto;}
	.xqInfor .cont view{padding-bottom: 20rpx;}
</style>
