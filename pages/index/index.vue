<template>
	<view>
		
		<view class="mglr4">
			<view class="pdt10 flexRowBetween">
				<view class="">
					<view class="fs12 color9">12月12日 星期二</view>
					<view class="fs16">Today</view>
				</view>
				<view class="flexEnd" @click="Router.navigateTo({route:{path:'/pages/personScreen/personScreen'}})">
					<image style="width: 30rpx;height: 22rpx;" src="../../static/images/home-icon.png" mode=""></image>
					<text class="mgl5">选择</text>
				</view>
			</view>
		
			<view class="banner-box">
				<view class="banner pdtb15">
					<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#0a6b67">
						<block v-for="(item,index) in labelData" :key="index">
							<swiper-item class="swiper-item" @click="Router.navigateTo({route:{path:'/pages/detail/detail'}})">
								<image :src="item" class="slide-image" />
							</swiper-item>
						</block>
					</swiper>
				</view>
			</view>
			
			<view class="personList">
				<view class="item boxShaow" v-for="(item,index) in personDate" :key="index">
					<view class="picbox" @click="Router.navigateTo({route:{path:'/pages/personInfor/personInfor'}})">
						<image class="pic" src="../../static/images/home-img.png" mode=""></image>
						<view class="fixInfor flexRowBetween white fs12">
							<view class="flex">
								<image class="photo" src="../../static/images/user-icon.png" mode=""></image>
								<text>NO.1025</text>
							</view>
							<view class="flexEnd">
								<image class="xin" src="../../static/images/home-icon1.png" mode=""></image>
								<text>4</text>
							</view>
						</view>
					</view>
					<view class="pdlr4 infor pdb15 color6">
						<view class="flexRowBetween titBox pdb10 pdt15">
							<view class="flex fs14 ll">
								<text>张三</text>
								<text class="mgl10 mgr10">西安市·雁塔区</text>
								<text class="mgr10">1989年</text>
								<text>未婚</text>
							</view>
							<view class="rr flexEnd fs12 color9" @click="">
								<image class="seeIcon" src="../../static/images/home-icon3.png" mode=""></image>
								<text>456</text>
							</view>
						</view>
						<view class="fs13 avoidOverflow2">法规及是反过来胡椒粉第三轮后方可大是否会回访近肯定是开发孵化基地</view>
					</view>
					
				</view>
			</view>
			
		</view>
		
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1-a.png" />
				</view>
				<view class="text this-text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.navigateTo({route:{path:'/pages/myInfor/myInfor'}})">
				<view class="nav_img nav_two">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">&ensp;</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">我的</view>
			</view>
		</view>
		<!--底部tab键 end-->
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
				labelData: [
					"../../static/images/home-banner.png",
					"../../static/images/home-banner.png"
				],
				personDate: [{},{},{}]
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
	
	page{padding-bottom: 140rpx;}
	.swiper-box {height: 280rpx;box-sizing: border-box;overflow: hidden;border-radius: 24rpx;}
	.swiper-box swiper-item {width: 100%;}
	.swiper-box image{width: 100%;height: 100%;}

</style>
