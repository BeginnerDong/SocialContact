<template>
	<view v-if="isShow">
		
		<view class="mglr4">
			<view class="pr mgt15 whiteBj radius24 oh">
				<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#0a6b67">
					<block v-for="(item,index) in mainData.mainImg" :key="index">
						<swiper-item class="swiper-item">
							<image :src="item.url" class="slide-image" mode="aspectFill"/>
						</swiper-item>
					</block>
				</swiper>
				<view class="fixInfor flexEnd white fs12">
					<view class="flexEnd" @click="clickGood()">
						<image class="xin" v-if="mainData.likeMe.length>0&&mainData.likeMe[0].status==1" src="../../static/images/home-icon2.png" mode=""></image>
						<image class="xin" v-else src="../../static/images/home-icon1.png" mode=""></image>
						<text>{{mainData.like?mainData.like.count:0}}</text>
					</view>
				</view>
			</view>
			
			<!-- 个人信息 -->
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flexRowBetween ftw pdb15">
					<view class="fs16">{{mainData.name}}</view>
					<view class="fs15">NO.{{mainData.no}}</view>
				</view>
				<view class="fs13">
					<text class="mgr15">{{mainData.birthday}}</text>
					<text class="mgr15">{{mainData.constellation}}</text>
					<text class="mgr15">{{mainData.height}}</text>
					<text>{{mainData.weight}}</text>
				</view>
				<view class="inforList fs13">
					<view class="item flex">
						<view class="ll">职业：</view>
						<view class="rr flex">
							<view class="lableBtn">{{mainData.occupation}}</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">月薪：</view>
						<view class="rr flex">
							<view class="lableBtn">{{mainData.salary}}</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">学历：</view>
						<view class="rr flex">
							<view class="lableBtn">{{mainData.education}}</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">婚姻：</view>
						<view class="rr flex">
							<view class="lableBtn">{{mainData.marriage}}</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">现居：</view>
						<view class="rr flex">
							<view class="lableBtn">{{mainData.province}}{{mainData.city}}{{mainData.country}}</view>
						</view>
					</view>
					<view class="item flex">
						<view class="ll">来自：</view>
						<view class="rr flex">
							<view class="lableBtn">{{mainData.hometown}}</view>
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
					<view class="lableBtn" v-for="item in mainData.hobby">{{item}}</view>
					
				</view>
			</view>
			
			<!-- 个人介绍 -->
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flex">
					<view class="xianTit fs15 ftw">个人介绍</view>
				</view>
				<view class="fs13 pdt15">{{mainData.introduction}}</view>
			</view>
			
			<!-- 择偶标准 -->
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flex">
					<view class="xianTit fs15 ftw">择偶标准</view>
				</view>
				<view class="fs13 pdt15">
					<view class="mgb5">{{mainData.spouse_standard}}</view>
				</view>
			</view>
			
			<view class="whiteBj pdlr4 pdt20 pdb20 radius24 mgt15">
				<view class="flex">
					<view class="xianTit fs15 ftw">相册</view>
				</view>
				<view class="photoAlbum mgt15">
					<scroll-view scroll-x>
						<view class="item" v-for="(item,inde) in mainData.bannerImg">
							<image @click="previewImage(index)" :src="item.url" mode="aspectFill"></image>
						</view>
					</scroll-view>
				</view>
			</view>
			
			<view class="B-TwoBtn flexCenter">
				<button open-type="share" class="item flexCenter mgr25" style="background: #ff8b2d;">
					<image class="icon" src="../../static/images/details-icon.png" mode=""></image>分享
				</button>
				<view class="item flexCenter" v-if="!isMe"
				@click="Router.navigateTo({route:{path:'/pages/contactKefu/contactKefu'}})">
						<image class="icon" src="../../static/images/details-icon1.png" mode=""></image>联系TA
				</view>
				<view class="item flexCenter" v-if="isMe"
				@click="Router.navigateTo({route:{path:'/pages/myInforEdit/myInforEdit'}})">
						<image class="icon" src="../../static/images/data-icon7.png" mode=""></image>编辑
				</view>
			</view>
			
			
		</view>
		
	</view>
	<view style="width: 100%;text-align: center;margin-top: 100rpx;" v-else>
		功能暂时关闭~请谅解
	</view>

</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:{},
				labelData: [
					"../../static/images/home-img.png",
					"../../static/images/home-img.png"
				],
				isMe:false,
				isShow:false,
				user_no:''
			}
		},
		
		onLoad(options) {
			const self = this;
			if(options.user_no){
				self.user_no = options.user_no;
				self.isShow = true;
			};
			
			if(self.user_no==uni.getStorageSync('user_info').user_no){
				self.isMe = true
			};
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShareAppMessage(ops) {
			console.log(ops)
			const self = this;
			if (ops.from === 'button') {
				return {
					title: '金遇良缘-'+self.mainData.name,
					path: '/pages/index/index?user_no='+self.user_no, //点击分享的图片进到哪一个页面
					imageUrl:self.mainData.mainImg[0].url,
					success: function(res) {
						// 转发成功
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
			}else{
				return {
					title: '金玉良缘-'+self.mainData.name,
					path: '/pages/index/index?user_no='+self.user_no, //点击分享的图片进到哪一个页面
					imageUrl:self.mainData.mainImg[0].url,
					success: function(res) {
						// 转发成功
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
				console.log(ops.target)
			}
		},
		
		methods: {
			
			previewImage(index){
				const self = this;
				console.log(index);
				var urls = [];
				for (var i = 0; i < self.mainData.bannerImg.length; i++) {
					urls.push(self.mainData.bannerImg[i].url)
				}
				uni.previewImage({
					urls: urls,
					current:index,
					longPressActions: {
						itemList: ['发送给朋友', '保存图片', '收藏'],
						success: function(data) {
							console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
						},
						fail: function(err) {
							console.log(err.errMsg);
						}
					}
				});
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:self.user_no,
					user_type:0
				};
				postData.getAfter = {
					likeMe: {
						tableName: 'Log',
						searchItem: {
							status:['in',[1,-1]],
							type:1,
							user_no:wx.getStorageSync('user_info').user_no
						},
						middleKey: 'user_no',
						key: 'relation_user',
						condition: 'in',
					},
					like: {
						tableName: 'Log',
						searchItem: {
							status:1,
							type:1,
						},
						middleKey: 'user_no',
						key: 'relation_user',
						condition: 'in',
						compute:{
						  count:[
						    'count',
						    'count',
						    {
						      status:1,
						    }
						  ]
						},
					},
				};
				postData.saveFunction = [{
					FuncName: 'viewUserInfo',
					searchItem:{
						user_no:self.user_no
					}
				}];
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						self.mainData.hobby = self.mainData.hobby.split(',')
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			clickGood() {
				const self = this;
				uni.setStorageSync('canClick', false);
					console.log(self.mainData.likeMe.length)
					
				if (self.mainData.likeMe.length == 0) {
					self.addGoodLog()
				} else {
					self.updateGoodLog()
				};
			},
			
			addGoodLog() {
				const self = this;
				const postData = {};
				postData.data = {
					type: 1,
					title: '收藏成功',
					relation_user: self.mainData.user_no,
					relation_table:'UserInfo',
					user_no: uni.getStorageSync('user_info').user_no,
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.mainData.likeMe.push({
							status: 1,
							id: res.info.id
						});
						self.mainData.like.count = self.mainData.like.count+1
						self.$Utils.showToast('已收藏', 'none', 1000)
					} else {
						self.$Utils.showToast('收藏失败', 'none', 1000)
					};
					uni.setStorageSync('canClick', true);	
				};
				self.$apis.logAdd(postData, callback);
			},
			
			
			updateGoodLog() {
				const self = this;
			
				const postData = {
					searchItem: {
						id: self.mainData.likeMe[0].id
						
					},
					data: {
						status: -self.mainData.likeMe[0].status
					}
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res.solely_code == 100000) {
						self.mainData.likeMe[0].status = -self.mainData.likeMe[0].status;
						if(self.mainData.likeMe[0].status==1){
							self.mainData.like.count = self.mainData.like.count+1
							self.$Utils.showToast('已收藏', 'none', 1000)
						}else{
							self.mainData.like.count = self.mainData.like.count-1
							self.$Utils.showToast('取消成功', 'none', 1000)
						}
					} else {
						self.$Utils.showToast(res.msg, 'none', 1000)
					};
				};
				self.$apis.logUpdate(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/personInfor.css";
	
	page{padding-bottom:180rpx;background: #f5f5f5;}
	button{
		background: none;
		line-height: 1.5;
		margin-left: 0;
		margin-right: 0;
		font-size: 15px;
	}
	button::after{
		border: none;
	}
</style>
