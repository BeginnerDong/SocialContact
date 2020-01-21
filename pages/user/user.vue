<template>
	<view v-if="showAll">
		<view class="whiteBj">
			<view class="userHead pdlr4">
				<view class="infor flexColumn">
					<view class="flexCenter" 
					style="width: 120rpx;height: 120rpx;border-radius: 50%;overflow: hidden;">
						<open-data type="userAvatarUrl"></open-data>
					</view>
					<view class="pdt10"><open-data type="userNickName"></open-data></view>
				</view>
			</view>
			
			<view class="myRowBetween mglr4 fs13" style="padding-top: 100rpx;">
				<view class="item flexRowBetween" @click="goPath()" v-if="kefuData.url!='1'">
					<view class="ll flex">
						<image class="icon" src="../../static/images/about-icon1.png" mode=""></image>
						<view class="">我的资料</view>
					</view>
					<view class="rr"><image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image></view>
				</view>
				<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/user-myCollect/user-myCollect'}})" >
					<view class="ll flex">
						<image class="icon" src="../../static/images/about-icon2.png" mode=""></image>
						<view class="">我的收藏</view>
					</view>
					<view class="rr"><image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image></view>
				</view>
				<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/contactKefu/contactKefu'}})" >
					<view class="ll flex">
						<image class="icon" src="../../static/images/about-icon3.png" mode=""></image>
						<view class="">联系客服</view>
					</view>
					<view class="rr"><image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image></view>
				</view>
				<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/user-set/user-set'}})" >
					<view class="ll flex">
						<image class="icon" src="../../static/images/about-icon4.png" mode=""></image>
						<view class="">设置</view>
					</view>
					<view class="rr"><image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image></view>
				</view>
			</view>
		</view>
		
			
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1.png" />
				</view>
				<view class="text">首页</view>
			</view>
			<view class="navbar_item" @click="goPath()" v-if="kefuData.url!='1'">
				<view class="nav_img nav_two">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">&ensp;</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3-a.png" />
				</view>
				<view class="text this-text">我的</view>
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
				score:'',
				wx_info:{},
				showAll:false,
				kefuData:{}
			}
		},
		
		onShow() {
			const self = this;
			const callback = (res) => {
					self.$Utils.loadAll(['getUserInfoData','getKefuData'], self);
			};
			self.$Token.getProjectToken(callback, {
				refreshToken: true
			})
		
		},
		
		methods: {
			
			goPath(){
				const self = this;
				if(self.userInfoData.gender!=''){
					self.Router.navigateTo({route:{path:'/pages/personInfor/personInfor?user_no='+uni.getStorageSync('user_info').user_no}})
				}else{
					self.Router.navigateTo({route:{path:'/pages/myInfor/myInfor'}})
				}
			},
			
			getKefuData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					title:'客服',
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.kefuData = res.info.data[0]
						self.showAll = true
					}
					self.$Utils.finishFunc('getKefuData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getUserInfoData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0];
					}
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.userInfoGet(postData, callback);
			},

		},
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	@import "../../assets/style/navbar.css";
	.userHead{height: 280rpx;background: url(../../static/images/about-icon.png) no-repeat 0 0 /100% 100%;}
	.userHead .infor{padding-top: 160rpx;}
	.userPhoto{width: 120rpx;height: 120rpx;border-radius: 50%;display: block;}
	
	.myRowBetween .ll .icon{width: 32rpx;height: 32rpx;margin-right: 20rpx;}
	
</style>
