<template>
	<view>
		
		<view class="mglr4">
			<view class="pr mgt15 whiteBj radius24 oh">
				<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#0a6b67">
					<block v-for="(item,index) in labelData" :key="index">
						<swiper-item class="swiper-item">
							<image :src="item" class="slide-image" />
						</swiper-item>
					</block>
				</swiper>
				<view class="fixInfor flexEnd white fs12">
					<view class="flexEnd">
						<image class="xin" src="../../static/images/home-icon1.png" mode=""></image>
						<text>4</text>
					</view>
				</view>
			</view>
			
			<!-- 个人信息 -->
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flexRowBetween ftw pdb15">
					<view class="fs16">张贤</view>
					<view class="fs15">NO.1023</view>
				</view>
				<view class="fs13">
					<text class="mgr15">1992.06</text>
					<text class="mgr15">金牛座</text>
					<text class="mgr15">160cm</text>
					<text>50kg</text>
				</view>
				<view class="inforList fs13">
					<view class="item flex">
						<view class="ll">职业：</view>
						<view class="rr flex">
							<view class="lableBtn">会计</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">月薪：</view>
						<view class="rr flex">
							<view class="lableBtn">4000</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">学历：</view>
						<view class="rr flex">
							<view class="lableBtn">本科</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">婚姻：</view>
						<view class="rr flex">
							<view class="lableBtn">未婚</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">现居：</view>
						<view class="rr flex">
							<view class="lableBtn">陕西省，西安市，长安区</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">来自：</view>
						<view class="rr flex">
							<view class="lableBtn">陕西省，西安市，长安区</view>
						</view>
					</view>
				</view>
			</view>
			
			<!-- 兴趣爱好 -->
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flex">
					<view class="xianTit fs15 ftw">兴趣爱好</view>
				</view>
				<view class="flex fs13 likeLable">
					<view class="lableBtn">旅行</view>
					<view class="lableBtn">摄影</view>
					<view class="lableBtn">游戏</view>
				</view>
			</view>
			
			<!-- 个人介绍 -->
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flex">
					<view class="xianTit fs15 ftw">个人介绍</view>
				</view>
				<view class="fs13 pdt15">个人介绍信息复合大师克利夫兰好伐很干净开发商打老虎刚刚看了后收代理费后尽快挂号费打了个讽德诵功法国人是刚发的发我给他人㔿发的是停一天刚发规范</view>
			</view>
			
			<!-- 择偶标准 -->
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flex">
					<view class="xianTit fs15 ftw">择偶标准</view>
				</view>
				<view class="fs13 pdt15">
					<view class="mgb5">1、放寒假课环和公交卡惊魂甫定申论两个和更进反馈个核桃仁太热</view>
					<view class="mgb5">2、刚发的花港饭店和回个电话回家还有人喊换接口科技一天挑事都是发才发的的论两个和更进反馈个核桃仁太热</view>
					<view class="mgb5">3、申论两个和更进反馈个核桃仁太热才发的还给她</view>
				</view>
			</view>
			
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flex">
					<view class="xianTit fs15 ftw">相册</view>
				</view>
				<view class="photoAlbum mgt15">
					<scroll-view scroll-x>
						<view class="item"><image src="../../static/images/details-img.png" mode=""></image></view>
						<view class="item"><image src="../../static/images/details-img.png" mode=""></image></view>
						<view class="item"><image src="../../static/images/details-img.png" mode=""></image></view>
						<view class="item"><image src="../../static/images/details-img.png" mode=""></image></view>
					</scroll-view>
				</view>
			</view>
			
			<view class="B-TwoBtn flexCenter">
				<view class="item flexCenter mgr25" style="background: #ff8b2d;">
					<image class="icon" src="../../static/images/details-icon.png" mode=""></image>分享
				</view>
				<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/myInforEdit/myInforEdit'}})">
						<image class="icon" src="../../static/images/data-icon7.png" mode=""></image>编辑
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
				labelData: [
					"../../static/images/home-img.png",
					"../../static/images/home-img.png"
				]
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
	@import "../../assets/style/personInfor.css";
	
	page{padding-bottom:180rpx;background: #f5f5f5;}
	
</style>
