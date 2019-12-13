<template>
	<view>
		
		<view class="mglr4">
			<view class="fs14 center pdt20 pdb10">协议</view>
			<view class="xqInfor fs12">
				<view>1、十个人刚刚很开发商的人发个回个话施工方如果黄金矿工收到货发个合同工法人就个发起。</view>
				<view>2、和赣服通的个话和公开了净空法师个帅哥换个方式的火锅华工科技六点十分火锅料鹤骨鸡肤还得给空港股份。</view>
				<view>3、沟通如果和很过分了说过话合格率三个人过节费是就废了的高房价的快感家乐福加工费。</view>
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
	@import "../../assets/style/editInfor.css";
	.xqInfor view{margin-bottom: 10rpx;}
</style>
