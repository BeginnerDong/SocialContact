<template>
	<view>
		
		<view class="mglr4 center pdt25 pdb20 ">
			<view class="fs13">客服微信</view>
			<image class="kf-ewm" :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''" mode=""></image>
		</view>
		<view class="f5H10"></view>
		<view class="mglr4 pdtb15 fs13">
			{{mainData.description}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[]
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
					title:'客服',
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0]
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.labelGet(postData, callback);
			},
		}
	};
</script>

<style>
	.kf-ewm{width: 280rpx;height: 280rpx;display: block;margin:0 auto ;}
</style>
