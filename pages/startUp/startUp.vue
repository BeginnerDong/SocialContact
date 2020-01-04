<template>
	<view>
		
		<view class="">
			<view class="bjPic"><image src="../../static/images/sartUp.png" mode=""></image></view>
		</view>
		<view class="flexColumn pdlr4 textBox">
			<view class="fs20 ftw">社交交友</view>
			<view class="fs13 color6 pdt15">一路前行，不只有你</view>
			<view class="enterBtn center fs13 pubBj" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">点击进入</view>
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
.bjPic image{width: 100%;height: 840rpx;}
.textBox{padding-top: 70rpx;}
.enterBtn{width: 200rpx;line-height: 60rpx;border-radius: 30rpx;color: #fff;margin-top: 70rpx;}
</style>
