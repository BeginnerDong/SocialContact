<template>
	<view>
		
		<view class="mglr4 center pdt25 pdb20 ">
			<view class="fs13">客服微信</view>
			<image class="kf-ewm" src="../../static/images/kefu-img.png" mode=""></image>
		</view>
		<view class="f5H10"></view>
		<view class="mglr4 pdtb15 fs13">和发的是两份工行和公交卡开发商来管理费供货方时间过来更好地发水立方嘎嘎让和公交卡快乐时光了干活该基金开放时代光华黑色仍然是多少价格</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				wx_info:{},
				is_show:false
			}
		},
		
		onLoad() {
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
		}
	};
</script>

<style>
	.kf-ewm{width: 280rpx;height: 280rpx;display: block;margin:0 auto ;}
</style>
