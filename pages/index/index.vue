<template>
	<view v-if="showAll">
		
		<view class="mglr4">
			<view class="pdt10 flexRowBetween">
				<view class="">
					<view class="fs12 color9">{{dateStr}}</view>
					<view class="fs16">Today</view>
				</view>
				<view class="flexEnd" v-if="kefuData.url!='1'"
				@click="Router.navigateTo({route:{path:'/pages/personScreen/personScreen'}})">
					<image style="width: 30rpx;height: 22rpx;" src="../../static/images/home-icon.png" mode=""></image>
					<text class="mgl5">选择</text>
				</view>
			</view>
		
			<view class="banner-box">
				<view class="banner pdtb15">
					<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#0a6b67">
						<block v-for="(item,index) in sliderData" :key="index">
							<swiper-item class="swiper-item" :data-id="item.id"
							@click="Router.navigateTo({route:{path:'/pages/detail/detail?id='+$event.currentTarget.dataset.id}})">
								<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="slide-image" />
							</swiper-item>
						</block>
					</swiper>
				</view>
			</view>
			
			<view class="personList" v-if="kefuData.url!='1'">
				<view class="item boxShaow"  v-for="(item,index) in mainData" :key="index">
					<view class="picbox">
						<image :data-user_no="item.user_no" 
						@click="Router.navigateTo({route:{path:'/pages/personInfor/personInfor?user_no='+$event.currentTarget.dataset.user_no}})" 
						class="pic" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode="aspectFill"></image>
						<view class="fixInfor flexRowBetween white fs12">
							<view class="flex">
								<image class="photo" :src="item.headImg" mode=""></image>
								<text>NO.{{item.no}}</text>
							</view>
							<view class="flexEnd" @click="clickGood(index)">
								<image class="xin" :src="item.likeMe.length>0&&item.likeMe[0].status==1?'../../static/images/home-icon2.png':'../../static/images/home-icon1.png'" mode=""></image>
								 <text>{{item.like?item.like.count:0}}</text>
							</view>
						</view>
					</view>
					<view class="pdlr4 infor pdb15 color6">
						<view class="flexRowBetween titBox pdb10 pdt15">
							<view class="flex fs14 ll">
								<text>{{item.name}}</text>
								<text class="mgl10 mgr10">{{item.city}}·{{item.country}}</text>
								<text class="mgr10">{{item.age}}岁</text>
								<text>{{item.marriage}}</text>
							</view>
							<view class="rr flexEnd fs12 color9" @click="">
								<image class="seeIcon" src="../../static/images/home-icon3.png" mode=""></image>
								<text>{{item.view_count}}</text>
							</view>
						</view>
						<view class="fs13 avoidOverflow2">{{item.introduction}}</view>
					</view>
				</view>
			</view>
			<view class="personList"  v-else>
				<view class="ind_proList">
					<view class="item flexRowBetween" :data-id="item.id" v-for="(item,index) in artData" :key="index" 
					@click="Router.navigateTo({route:{path:'/pages/detail/detail?id='+$event.currentTarget.dataset.id}})">
						<view class="ll">
							<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
						</view>
						<view class="rr">
							<view class="avoidOverflow title">{{item.title}}</view>
							<view class="avoidOverflow2 color3 font13 text">{{item.description}}</view>
							<view class="data">{{item.create_time}}</view>
						</view>
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
			<view class="navbar_item" @click="goPath()" v-if="kefuData.url!='1'">
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
				Utils:this.$Utils,
				searchItem:{
					user_type:0,
					check:1
				},
				showAll:false,
				dateStr:'',
				sliderData:[],
				mainData:[],
				search:{
					gender:'',
					age:'',
					education:'',
					address:[]
				},
				kefuData:{},
				artData:[]
			}
		},
		
		onLoad(options) {
			const self = this;
			if(options.user_no){
				self.Router.navigateTo({route:{path:'/pages/personInfor/personInfor?user_no='+options.user_no}})
			};
			self.dateStr = self.$Utils.getCurrentDate();
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			const callback = (res) => {
				self.$Utils.loadAll(['getMainData','getUserData','getSliderData','getKefuData','getArtData'], self);
			};
			self.$Token.getProjectToken(callback, {
				refreshToken: true
			});
			
			uni.setStorageSync('search',self.search)
		},
		
		onShow() {
			const self = this;
			self.searchItem = {
				user_type:0,
				check:1
			};
			self.search = uni.getStorageSync('search',self.search);
			console.log(self.search)
			if(self.search.education!=''){
				self.searchItem.education = self.search.education
			};
			if(self.search.gender!=''){
				if(self.search.gender=='男'){
					self.searchItem.gender = 1
				}else{
					self.searchItem.gender = 2
				}
			};
			if(self.search.age!=''){
				console.log(self.search.age.split('-'))
				self.searchItem.age = ['between',[parseInt(self.search.age.split('-')[0]),parseInt(self.search.age.split('-')[1])]]
			};
			if(self.search.address.length>0){
				//self.searchItem.province = self.search.address[0];
				self.searchItem.city = self.search.address[0];
				self.searchItem.country = self.search.address[1];
			};
			if(uni.getStorageSync('isNew')&&uni.getStorageSync('isNew')==true){
				self.getMainData(true)
			}
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		 onPullDownRefresh() {
			const self = this;
			console.log('refresh');
			delete self.searchItem.gender;
			delete self.searchItem.age;
			delete self.searchItem.education;
		
			delete self.searchItem.city;
			delete self.searchItem.country;
		
			self.getMainData(true)	
		},
		
		methods: {
			
			getArtData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2
				};
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['=', ['新闻']],
						},
						condition:'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.artData.push.apply(self.artData,res.info.data)
					}
					console.log(self.artData)
					self.$Utils.finishFunc('getArtData');
				};
				self.$apis.articleGet(postData, callback);
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
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 5
					}
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
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
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					if(uni.getStorageSync('isNew')){
						uni.setStorageSync('isNew',false)
					};
					uni.stopPullDownRefresh();
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			getSliderData() {
				const self = this;
				const postData = {};
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['=', ['首页轮播']],
						},
						condition:'in'
					}
				};
				postData.searchItem = {
					thirdapp_id:2
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.sliderData.push.apply(self.sliderData,res.info.data)
					}
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						/* if(self.userData.headImgUrl==''){
							self.Router.redirectTo({route:{path:'/pages/startUp/startUp'}})
						}else{
							self.userInfoUpdate()
						} */
						self.userInfoUpdate()
					}
				};
				self.$apis.userGet(postData, callback);
			},
			
			goPath(){
				const self = this;
				if(self.userData.info.gender!=''){
					self.Router.navigateTo({route:{path:'/pages/myInforEdit/myInforEdit'}})
				}else{
					self.Router.navigateTo({route:{path:'/pages/myInfor/myInfor'}})
				}
			},
			
			userInfoUpdate() {
				const self = this;
				uni.showLoading({
					title: '更新数据中',
					mask: true
				});
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				postData.data = {
					headImg:self.userData.headImgUrl
				};
				const callback = (res) => {
					if (res.solely_code == 100000) {
						
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
			
			
			clickGood(index) {
				const self = this;
				uni.setStorageSync('canClick', false);	
				if (self.mainData[index].likeMe.length == 0) {
					self.addGoodLog(index)
				} else {
					self.updateGoodLog(index)
				};
			},
			
			addGoodLog(index) {
				const self = this;
				const postData = {};
				postData.data = {
					type: 1,
					title: '收藏成功',
					relation_user: self.mainData[index].user_no,
					relation_table:'UserInfo',
					user_no: uni.getStorageSync('user_info').user_no,
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.mainData[index].likeMe.push({
							status: 1,
							id: res.info.id
						});
						self.mainData[index].like.count = self.mainData[index].like.count+1
						self.$Utils.showToast('已收藏', 'none', 1000)
					} else {
						self.$Utils.showToast('收藏失败', 'none', 1000)
					};
					uni.setStorageSync('canClick', true);	
				};
				self.$apis.logAdd(postData, callback);
			},
			
			
			updateGoodLog(index) {
				const self = this;
			
				const postData = {
					searchItem: {
						id: self.mainData[index].likeMe[0].id
						
					},
					data: {
						status: -self.mainData[index].likeMe[0].status
					}
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res.solely_code == 100000) {
						self.mainData[index].likeMe[0].status = -self.mainData[index].likeMe[0].status;
						if(self.mainData[index].likeMe[0].status==1){
							self.mainData[index].like.count = self.mainData[index].like.count+1
							self.$Utils.showToast('已收藏', 'none', 1000)
						}else{
							self.mainData[index].like.count = self.mainData[index].like.count-1
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
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/personList.css";
	
	page{padding-bottom: 140rpx;}
	.swiper-box {height: 280rpx;box-sizing: border-box;overflow: hidden;border-radius: 24rpx;}
	.swiper-box swiper-item {width: 100%;}
	.swiper-box image{width: 100%;height: 100%;}
	.ind_proList .item{padding:30rpx 0;border-bottom: 2rpx solid #e7e7e7; align-items: normal;}
	.ind_proList .item .ll{width: 250rpx; height: 166rpx; overflow: hidden;}
	.ind_proList .item .ll image{width: 100%; height: 100%; display: block;}
	.ind_proList .item .rr{width: 420rpx;height: 166rpx;position: relative;}
	.ind_proList .item .title{font-size: 26rpx; line-height: 36rpx;}
	.ind_proList .item .text{font-size: 24rpx;line-height: 32rpx; padding-top: 10rpx;}
	.ind_proList .item .data{position: absolute;bottom: 0;left: 0; width: 100%;box-sizing: border-box; color: #999; font-size: 24rpx;}
	.ind_proList .item .money{position: absolute;bottom: 0;left: 0; width: 100%;box-sizing: border-box; color: #999; font-size: 28rpx;}
</style>
