<template>
	<view>

		<view class="mglr4 center pdt25 pdb20 ">
			<view class="fs13">{{mainData.description&&mainData.description!=''?mainData.description:''}}</view>

			<image v-for="(item,index) in mainData.mainImg" @click="previewImage(index)" class="kf-ewm" :src="item.url" mode=""></image>
		</view>
		<view class="f5H10"></view>
		<!-- <view class="mglr4 pdtb15 fs13" v-if="mainData.description!=''">
			{{mainData.description&&mainData.description!=''?mainData.description:''}}
		</view> -->
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

		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {

			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					title: '客服',
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0]
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.labelGet(postData, callback);
			},

			previewImage(index) {
				console.log(1);
				const self = this;
				var urls = [];
				for (var i = 0; i < self.mainData.mainImg.length; i++) {
					urls.push(self.mainData.mainImg[i].url)
				};
				var current = self.mainData.mainImg[index].url; //这里获取到的是一张本地的图片
				wx.previewImage({
					current: current, //需要预览的图片链接列表
					urls: urls //当前显示图片的链接
				})
			},

		}
	};
</script>

<style>
	.kf-ewm {
		width: 500rpx;
		height: 500rpx;
		display: block;
		margin: 20rpx auto;
	}
</style>
