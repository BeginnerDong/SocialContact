<template>
	<view>
		
		<view class="myRowBetween pdlr4 whiteBj">
			<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/user-help/user-help'}})">
				<view class="ll">帮助与反馈</view>
				<view class="rr"><image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image></view>
			</view>
			<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/user-xieyi/user-xieyi'}})">
				<view class="ll">用户协议</view>
				<view class="rr"><image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image></view>
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
	page{background: #F5F5F5;}
</style>
