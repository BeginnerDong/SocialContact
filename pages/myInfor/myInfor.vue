<template>
	<view>
		
		<view class="cont">
			<view class="center mgb30">你是</view>
			<view class="selt-sex fs13 flexRowBetween center">
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/myInforEdit/myInforEdit'}})">
					<view class="photo"  >
						<image class="pto" :src="curr==1?'../../static/images/data-icon2.png':'../../static/images/data-icon.png'" mode=""></image>
					</view>
					<view class="pdt10">男生</view>
				</view>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/myInforEdit/myInforEdit'}})">
					<view class="photo">
						<image class="pto" :src="curr==2?'../../static/images/data-icon3.png':'../../static/images/data-icon1.png'" mode=""></image>
					</view>
					<view class="pdt10">女生</view>
				</view>
			</view>
			<view class="myInfor">
				<view class="item flex">
					<view class="ll"><image class="icon" src="../../static/images/data-icon4.png" mode=""></image></view>
					<view class="rr">
						<view class="tit">数据保密</view>
						<view class="tex">您的信息我们将严格保密</view>
					</view>
				</view>
				<view class="item flex">
					<view class="ll"><image class="icon" src="../../static/images/data-icon5.png" mode=""></image></view>
					<view class="rr">
						<view class="tit">完善信息</view>
						<view class="tex">认真完善您的个人信息</view>
					</view>
				</view>
				<view class="item flex">
					<view class="ll"><image class="icon" src="../../static/images/data-icon6.png" mode=""></image></view>
					<view class="rr">
						<view class="tit">认证优先</view>
						<view class="tex">请联系客服认证</view>
					</view>
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
				is_show:false,
				curr:0
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		mounted() {
			// 导航当前项
			const self = this;
			var pages = getCurrentPages();
			var page = pages[pages.length - 1].route;
			console.log('222',page)
			if(page=='pages/myInforEdit/myInforEdit'){
				self.curr=1
			}else if(page=='pages/myInforEdit/myInforEdit'){
				self.curr=2
			}
		},
		methods: {
			// currSex(curr){
			// 	const self = this;
			// 	if(curr!=self.curr){
			// 		self.curr = curr
			// 	}
			// },
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
	.cont{padding:80rpx 18%;}
	.selt-sex{margin-bottom: 70rpx;}
	.selt-sex .photo{width: 152rpx;height: 152rpx;}
	.selt-sex .photo .pto{width: 100%;height: 100%;display: block;}
	
	.myInfor .item{margin-bottom: 50rpx;}
	.myInfor .ll{width: 20%;}
	.myInfor .rr{width: 80%;}
	.myInfor .ll .icon{width: 80rpx;height: 80rpx;}
	.myInfor .tit{font-size: 26rpx;}
	.myInfor .tex{font-size: 24rpx;color: #666;}
</style>
