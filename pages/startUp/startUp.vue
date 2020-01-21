<template>
	<view>
		
		<view class="">
			<view class="bjPic"><image src="../../static/images/sartUp.png" mode=""></image></view>
		</view>
		<view class="flexColumn pdlr4 textBox">
			<view class="fs20 ftw">社交交友</view>
			<view class="fs13 color6 pdt15">一路前行，不只有你</view>
			<button class="enterBtn center fs13 pubBj" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">点击进入</button>
		</view>
		
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				wx_info:{},
				Utils:this.$Utils
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				const callback = (user, res) => {
					self.Router.redirectTo({route:{path:'/pages/index/index'}})
				};
				self.$Utils.getAuthSetting(callback);	
			},
			
			
		}
	};
</script>

<style>
.bjPic image{width: 100%;height: 840rpx;}
.textBox{padding-top: 70rpx;}
.enterBtn{width: 200rpx;line-height: 60rpx;border-radius: 30rpx;color: #fff;margin-top: 70rpx;}
</style>
