<template>
	<view>
		
		<view class="questionList fs13">
			<view class="item" v-for="(item,index) in questionDate" :key="index">
				<view class="flex line">
					<view class="ll"><image class="icon" src="../../static/images/help-icon.png" mode=""></image></view>
					<view class="rr">刚发的刚发的花港饭店？</view>
				</view>
				<view class="flex line mgt5">
					<view class="ll"><image class="icon" src="../../static/images/help-icon1.png" mode=""></image></view>
					<view class="rr color6">个就是感觉就管理会计发的是根据风格我锦江股份了上东国际结果翻到了好几个的就好了股东会？</view>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view>没找到问题，咨询客服</view>
				<view @click="Router.navigateTo({route:{path:'/pages/contactKefu/contactKefu'}})"><image class="kefuIcon" src="../../static/images/help-icon2.png" mode=""></image></view>
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
				is_show:false,
				questionDate:['','','','']
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
	.questionList .item{padding: 30rpx 4%;border-bottom: 10rpx solid #F5F5F5;}
	.questionList .item .line{align-items: flex-start;}
	.questionList .ll{width: 50rpx;}
	.questionList .ll .icon{width: 28rpx;height: 28rpx;}
	.questionList .rr{width: 92%;}
	
	.kefuIcon{width: 60rpx;height: 54rpx;}
</style>
