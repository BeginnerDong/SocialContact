<template>
	<view>
		
		<view class="pdlr4 myInforEdit mgt15">
			<view class="item">
				<view class="tit">你的姓名？</view>
				<view class="flexRowBetween fs12">
					<view class="text">可填写昵称！</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的出生年月？</view>
				<view class="flexRowBetween fs12">
					<view class="text">会推算您的年龄噢！</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的星座？</view>
				<view class="flexRowBetween fs12">
					<view class="text">看哪个星座和你更匹配</view>
					<view class="flexEnd rr">
						<text class="color9">请选择</text>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的身高？</view>
				<view class="flexRowBetween fs12">
					<view class="text">异性有时候看重身高</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">你的体重？</view>
				<view class="flexRowBetween fs12">
					<view class="text">异性有时候很在意体重</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的学历？</view>
				<view class="flexRowBetween fs12">
					<view class="text">更好的展示自己</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">婚姻状况？</view>
				<view class="flexRowBetween fs12">
					<view class="text">严格审核婚姻，酒托</view>
					<view class="flexEnd rr">
						<text class="color9">请选择</text>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的籍贯？</view>
				<view class="flexRowBetween fs12">
					<view class="text">三百年前是一家</view>
					<view class="flexEnd rr">
						<text class="color9">请选择</text>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你工作生活在？</view>
				<view class="flexRowBetween fs12">
					<view class="text">可以一起约个饭</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的职业？</view>
				<view class="flexRowBetween fs12">
					<view class="text">异性有时很在乎职业</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的微信？</view>
				<view class="flexRowBetween fs12">
					<view class="text">方便心动的TA联系你</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的手机号？</view>
				<view class="flexRowBetween fs12">
					<view class="text">方便心动的TA联系你</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的月收入？</view>
				<view class="flexRowBetween fs12">
					<view class="text">其实人品更重要</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">房车情况？</view>
				<view class="flexRowBetween fs12">
					<view class="text">更好的找到那个TA</view>
					<view class="flexEnd rr">
						<input type="text" value="" />
					</view>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">你的兴趣爱好？<text class="fs12 color9">让那个TA更好的了解你</text></view>
				<view class="likeLable flex fs12 color6">
					<view class="btn" :class="{on:item.selt}" @click="checkLike(index)" v-for="(item,index) in likeLable" :key="index">{{item.title}}</view>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">个人介绍<text class="fs12 color9 mgl5">让那个TA更了解你</text></view>
				<view class="fs12 color6 mgt10">
					<textarea class="f5bj radius10" style="height: 200rpx;" value="" placeholder="请输入" placeholder-class="placeholder"/>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">择偶标准<text class="fs12 color9 mgl5">更好的找到那个TA</text></view>
				<view class="fs12 color6 mgt10">
					<textarea class="f5bj radius10" style="height: 200rpx;" value="" placeholder="请输入" placeholder-class="placeholder"/>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">相册<text class="fs13 mgl10">(可上传多张)</text></view>
				<view class="fs12 color6 mgt10 upPhoto flex mgt10">
					<view class="lis">
						<image src="../../static/images/data-icon9.png" mode=""></image>
					</view>
					<view class="lis">
						<image src="../../static/images/details-img.png" mode=""></image>
					</view>
					<view class="lis">
						<image src="../../static/images/details-img.png" mode=""></image>
					</view>
					<view class="lis">
						<image src="../../static/images/details-img.png" mode=""></image>
					</view>
				</view>
			</view>
			
		</view>
		
		<view class="submitbtn pdtb25">
			<button class="btn" type="button" @click="Router.navigateTo({route:{path:'/pages/myInforCont/myInforCont'}})">确定</button>
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
				likeLable:[
					{title:'旅行',selt:false},
					{title:'摄影',selt:false},
					{title:'游戏',selt:false},
					{title:'看书',selt:false},
					{title:'逛街',selt:false},
					{title:'美食',selt:false},
					{title:'运动',selt:false},
					{title:'音乐',selt:false}
				]
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			checkLike(i){
				const self = this;
				self.likeLable[i].selt = !self.likeLable[i].selt
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
	.myInforEdit .item{padding: 30rpx 4%;border-radius: 10rpx;box-shadow: 0 0 10rpx rgba(0,0,0,0.1);background: #FFF;margin-bottom: 30rpx;}
	.myInforEdit .item .tit{font-size:30rpx; margin-bottom: 10rpx;}
	.myInforEdit .item .text{width: 55%;color: #999;}
	.myInforEdit .item .rr{width: 200rpx;border-bottom: 1px solid #0A6B67;padding-bottom: 4rpx;padding: 0 10rpx;box-sizing: border-box;padding-bottom: 4rpx;}
	.myInforEdit .item .rr input{width: 100%;line-height: 20rpx;display: block;text-align: right;padding: 0 10rpx;box-sizing: border-box;font-size: 24rpx;color: #666;}
	
	.likeLable{flex-wrap: wrap;}
	.likeLable .btn{min-width: 140rpx;text-align: center;line-height: 50rpx;border-radius: 30rpx;border:1px solid #cdcdcd;box-sizing: border-box;padding: 0 30rpx;margin-right:22rpx; margin-top: 30rpx;}
	.likeLable .btn:nth-of-type(4n){margin-right: 0;}
	.likeLable .btn.on{background: #0A6B67;color: #fff;border-color:#0A6B67;}
	
	.upPhoto{flex-wrap: wrap;}
	.upPhoto .lis{width:200rpx;height: 140rpx;overflow: hidden;margin:0 16rpx 16rpx 0;}
	.upPhoto .lis image{width: 100%;height: 100%;}
	.upPhoto .lis:nth-of-type(3n){margin-right: 0;}
</style>
