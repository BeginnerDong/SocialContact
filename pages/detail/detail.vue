<template>
	<view>
		
		<view class="detailxqBan">
			<image src="../../static/images/event-details-img.png" mode=""></image>
		</view>
		<view class="xqInfor mglr4 pdt20">
			<view class="title">
				<view class="center fs14">标题标题标题标题标题标题</view>
				<view class="fs13 color6 pdt10 flexEnd" >2019.12.12</view>
			</view>
			<view class="cont pdt15 fs13">
				<view>会发生的进口量很过分过会就快乐十分和归属感广寒深宫服饰老钢供货方收点费还是个个会发生了干活付给过会就发的是。</view>
				<view>会发生的进口量很过分过会就快乐十分和归属感广寒深宫服饰老钢供货方收点费还是个个会发生了干活付给过会就发热体。</view>
				<view>会发生的进口量很过分过会就快乐十分和归属感广寒深宫服饰老钢供货方收点费还是个个会发生了干活付给过会就个国际饭店估计富商大贾管天管地。</view>
				<view>
					<image src="../../static/images/event-details-img1.png" mode="widthFix"></image>
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
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/personList.css";
	
	page{padding-bottom:60rpx;}
	
	.detailxqBan{ width: 100%;height: 400rpx; display: block;}
	.detailxqBan image{ width: 100%; height: 100%; display: block;}
	
	.xqInfor .cont image{max-width: 100% !important; display: block;margin:20rpx auto;}
	.xqInfor .cont view{padding-bottom: 20rpx;}
</style>
