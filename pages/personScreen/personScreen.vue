<template>
	<view>
		
		<view class="mglr4">
			<view class="myRowBetween fs13">
				<view class="item flexRowBetween">
					<view class="ll">性别</view>
					<view class="rr" @click="sexShow">
						<text class="color9">请选择</text>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
				<view class="item flexRowBetween">
					<view class="ll">年龄</view>
					<view class="rr" @click="ageShow">
						<text class="color9">请选择</text>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
				<view class="item flexRowBetween">
					<view class="ll">学历</view>
					<view class="rr" @click="educationShow">
						<text class="color9">请选择</text>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
				<view class="item flexRowBetween">
					<view class="ll">地区</view>
					<view class="rr">
						<text class="color9">请选择</text>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="flexEnd pdtb15">
				<view class="tagBtn fs12 color6">重置</view>
			</view>
			
			<view class="submitbtn" style="margin-top: 200rpx;">
				<button class="btn" type="button">确定</button>
			</view>
			
			<view class="black-bj" v-show="is_show"></view>
			
			<!-- 性别选择 -->
			<view class="alertShow radius10" v-show="is_sexShow">
				<view class="item" @click="sexShow" v-for="(item,index) in sexDate" :key="index" >{{item}}</view>
			</view>
			
			<!-- 年龄选择 -->
			<view class="alertShow radius10" v-show="is_ageShow">
				<view class="item" @click="ageShow" v-for="(item,index) in ageDate" :key="index" >{{item}}</view>
			</view>
			
			<!-- 年龄选择 -->
			<view class="alertShow radius10" v-show="is_educationShow">
				<view class="item" @click="educationShow" v-for="(item,index) in educationDate" :key="index" >{{item}}</view>
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
				is_sexShow:false,
				sexDate:['男','女'],
				is_ageShow:false,
				ageDate:['18-24岁','24岁-30岁','30-38岁','38岁以上'],
				is_educationShow:false,
				educationDate:['高中及高中以下学历','大专','本科','研究生及研究生以上']
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			sexShow(){
				const self = this;
				self.is_show = !self.is_show
				self.is_sexShow = !self.is_sexShow
			},
			ageShow(){
				const self = this;
				self.is_show = !self.is_show
				self.is_ageShow = !self.is_ageShow
			},
			educationShow(){
				const self = this;
				self.is_show = !self.is_show
				self.is_educationShow = !self.is_educationShow
			},
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
	
	.tagBtn{width: 120rpx;line-height: 50rpx;border-radius: 30rpx;background: #ececec;text-align: center;}
	.alertShow{width: 80%;background: #fff;position:fixed ;top: 50%;left: 50%;z-index: 60;transform: translate(-50%,-50%);}
	.alertShow .item{padding: 30rpx 5%;border-bottom: 1px solid #eee;}
	.alertShow .item:last-child{border-bottom: 0;}
</style>
